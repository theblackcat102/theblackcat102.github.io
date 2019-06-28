## XLNet: Generalized Autoregressive Pretraining for Language Understanding

在過去自然語言 (NLP) state of the art (SOTA) 的模型如 ：GPT, BERT 中還未解決的問題如下：

1. Transformer 句子長度限制
    在過往的NLP 模型中，尤其 Transformer 模型，句子的長度往往受限於模型的sequence length 長度影響。在 Transformer 模型的訓練過程中，如果有一個很長的順序無法在一次 feedforward 內完成，一般上會分為數段來做。然而每一段之間的 hidden state 並沒有共享。
2. BERT 預訓練差異問題
    在 BERT 的目標函數：
                                $$max \sum_{t=1}^T  m_{t}  log p_{\theta}(x_{t} | x_{1..t-1})$$ 
    其中 mask $$m_{t}$$ 會是 0 或 1，BERT 的目的。在考慮每個 mask $$m_{t}$$ 的值是獨立存在的。但是每個文字都有相依性例如 New York is a city，在 BERT 中如果被屏蔽掉 New、 York 這兩個字（就是輸入的句子中New、York 二字被取代成 “MASK”，模型在預訓練需要學習從 “MASK”還原回原字），損失函數會只會學習到這兩個函數 $$p(New | is, a, city)$$, $$p(York | is, a, city)$$  而學習不了 New 與 York 的關係。
3. 傳統自回歸（ AR ）訓練方式無法學習雙向關係
    在傳統的自回歸學習中，目前的輸出 $$y_t$$ 只是由 $$x_{1:t-1}$$ 的輸入決定，模型在一些回答問題、語言翻譯的資料上無法學習到關鍵資訊。

在XLNet 針對每個問題提出解決方法：

問題 1 ：
從 Transformer XL ：An attentive language model beyond fixed length context 這篇論文中，作者透過將 Transformer 區塊作為一個 RNN cell 的形式，使模型可以分段的解析超長的句子。

問題 2,3 ：

作者根據 NADE 的論文中提到，任意一個第$$d$$ 緯度可以由 $$1:d-1$$ 維度的因式分解組成，將目前需要補上的字與其他被屏蔽的字的關係也學習起來。如第二問題中舉例的 New York is a city。可以意因式分解的可能有： New → York → is → a → city, York → New → is → a → city, city → is → a → New → York *。接著再使用自回歸來學習這些句子的因式分解變形即可學習到前後文的資訊。如此一來，模型可以使用雙向設計學習句子前後的關係。

到這裡，XLNet 架構既結合了 AR 的優勢（預訓練於微調整資訊對等），也用到 BERT 的雙向 Transformer 結構但在預訓練階段不會有 MASK 的字出現。

*注意：這裡的文字調亂了，其 transformer 的 positional embedding 也會隨著調換，因為 self attention 在權重乘機上並沒有不會因為positional bias 而影響先後順序的概念。

（未完詳細機制我之後會陸續補上）
