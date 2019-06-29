---
keywords:
  - deep learning
  - neural network
  - SOTA
  - XLNet
  - 自然語言
  - 深度學習
comments: true
title : XLNet 超越GPT、BERT的自然語言模型
cover_image: https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/xlnet_cover_image.png
---


2019 年最新的論文 [XLNet: Generalized Autoregressive Pretraining for Language Understanding](https://arxiv.org/abs/1906.08237), 作者在結果中證實超越了目前 NLP 模型中最好的模型如 GPT, BERT。這裡就稍微解析一下為何 XLNet 的架構可以超越 GPT、BERT 模型吧～

在過去自然語言 (NLP) state of the art (SOTA) 的模型如 ：GPT, BERT 中還未解決的問題如下：

1. Transformer 句子長度限制
    在過往的NLP 模型中，尤其 Transformer 模型，句子的長度往往受限於模型的sequence length 長度影響。在 Transformer 模型的訓練過程中，如果有一個很長的順序無法在一次 feedforward 內完成，一般上會分為數段來做。然而每一段之間的 hidden state 並沒有共享。

2. BERT 預訓練與微調階段存在差異
    在 BERT 的目標函數：
                                $$max \sum_{t=1}^T  m_{t}  log p_{\theta}(x_{t} | x_{1..t-1})$$ 
    其中 mask $$m_{t}$$ 會是 0 或 1，BERT 的目的。在考慮每個 mask $$m_{t}$$ 的值是獨立存在的。但是每個文字都有相依性例如 New York is a city，在 BERT 中如果被屏蔽掉 New、 York 這兩個字（就是輸入的句子中New、York 二字被取代成 “MASK”，模型在預訓練需要學習從 “MASK”還原回原字），損失函數會只會學習到這兩個函數 $$p(New | is, a, city)$$, $$p(York | is, a, city)$$  而學習不了 New 與 York 的關係。此外 mask 的機制會讓模型在微調階段沒有 MASK 這個字而造成預訓練與微調輸入有落差的問題 (論文中稱作pretrain finetune discrepancy)。

3. 傳統自回歸（ AR ）訓練方式無法學習雙向關係
    在傳統的自回歸學習中，目前的輸出 $$y_t$$ 只是由 $$x_{1:t-1}$$ 的輸入決定，模型在一些回答問題、語言翻譯的資料上無法學習到關鍵資訊。

在XLNet 針對每個問題提出解決方法：

問題 1 ：
從 Transformer XL ：An attentive language model beyond fixed length context 這篇論文中，作者透過將 Transformer 區塊作為一個 RNN cell 的形式，使模型可以分段的解析超長的句子。

問題 2,3 ：

作者根據類神經網路自回歸密度估計 (NADE) 的論文中提到，任意一個第$$d$$ 緯度可以由 $$1:d-1$$ 維度的因式分解組成，將目前需要補上的字與其他被屏蔽的字的關係也學習起來。如第二問題中舉例的 New York is a city。可以意因式分解的可能有： New → York → is → a → city, York → New → is → a → city, city → is → a → New → York *。接著再使用自回歸來學習這些句子的因式分解變形即可學習到前後文的資訊。如果序列長度為 T 那麼其因式分解的結果會有 T! 種。如此一來，模型可以使用雙向設計學習句子前後的關係。

到這裡，XLNet 架構既結合了 AR 的優勢（預訓練於微調整資訊對等），也用到 BERT 的雙向 Transformer 結構但在預訓練階段不會有 MASK 的字出現。關於 NADE 的論文我在之前發文講解過有興趣的話可以[點過去看看](https://theblackcat102.github.io/%E9%A1%9E%E7%A5%9E%E7%B6%93%E7%B6%B2%E8%B7%AF%E8%87%AA%E5%9B%9E%E6%AD%B8%E5%AF%86%E5%BA%A6%E4%BC%B0%E8%A8%88-Neural-Autogressive-Density-Estimator/)。

*注意：這裡的文字調亂了，其 transformer 的 positional embedding 不會隨著調換，因為 self attention 在權重乘機上並沒有不會因為positional bias 而影響先後順序的概念。不理解的話可以參考以下 gif

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/output_fhhFZ2.gif#center)


## AR的因式分解

前段說過，XLNet 為了透過序列的因式分解學習不同文字之間的關係。使用一個 mask 來控制因式分解結果。

範例：
假設句子如 New York is a city，經過因式分級其中一個可能為 is a city New York。而今天屏蔽了 city, New, York 這三個字。

那麼當下的 loss 為

$$ L_{XLNet} = log_{p}( New | is a city  ) + log_{p}(city | ) + log_{p}(York | is a city New ) $$

第二種因式分解形式為 New York is a city，被屏蔽掉的字為 city。那麼當下的 loss 則是 

$$L_{XLNet} = log_{p}(city | New York is a )$$

## XLNet 隱藏層問題

由於目標函數需要看到雙向的資訊但使用過去 Transformer XL 中只有一個隱藏 $$h_{\theta}$$向量是有問題的。因為但憑之前的隱藏向量是沒有當前需要預測字的位置資訊，所以無論目標字在任何一個位置，預測結果依然一樣。

為此，XLNet 提出將過去的隱藏函數分為 1. 內容表達 $$h_{\theta}$$ 2. 查詢表達 $$g_{\theta}$$ 兩個隱藏向量。表達內容的向量 $$h_{\theta}$$ 與之前的 Transformer 一樣，既包含內容也包含預測目標的內容 $$ h_{\theta x <= t}  $$ 。查詢隱藏向量 $$g_{\theta}$$ 則只會包含過去 $$x_{ < t}$$ 資訊於當下 $$t$$ 的位置資訊 $$z_{t}$$。

比較好理解的就是架構變成有兩個共享權重的 Transformer ，差異是輸入一個有當下要預測目標位置的輸入資訊 $$x_{t} $$在隱藏層中表達為$$h$$ ，另一個輸入只有 $$x_{t}$$ 的位置資訊在隱藏層中表達為$$g$$。

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/xlnet_hidden_states.png#center)

## Transformer XL

XLNet 從 Transformer XL 的論文中使用了它的相對位置編碼機制（有別於一般 Transformer 的 cosine + sine 位置編碼），相對位置編碼只在乎位置 $$i$$、 $$j$$ 之相關值。另外也借用了將 Transformer 當成一個RNN中 recurrent cell 使用，用來處理超過傳統 Transformer 序列長度受限的問題。

詳細內容可以參考 Transformer XL 的論文： [arxiv.org/abs/1901.02860](https://arxiv.org/abs/1901.02860)

## 總結

XLNet 結合過往雙向 Transformer 與 Transformer 自序列訓練(AR)方法，並把 Transformer 表達成一個類似 RNN cell 的形式，解決了過去2017 年提出的第一代 Transformer 架構在處理序列資料的種種問題。刷新自然語言裡各種任務的新分數。

在完成這篇文章的同時微軟發表了新的論文 MASS : MAsked Sequence to Sequence 宣稱刷新 BERT 之前在語言翻譯的分數。但 XLNet 與 MASS 在實測結果中沒有一項任務是重疊可比較的（MASS 專注在語言翻譯，XLNet 專注在情感分析、分類、問答）。從我對 MASS 初略的理解，MASS的訓練與架構更接近 BERT，論文沒有解決Transformer 序列受限與pretrain-finetune discrepancy 的問題。雖然我認為後者對於結果其實影響應該不大，因為在fintune階段模型可以自我修正權重降低預訓練資料與真實資料的差異影響。



* [Pytorch 實作 XLNet](https://github.com/graykode/xlnet-Pytorch)

* [原本論文：arxiv.org/abs/1906.08237 ](https://arxiv.org/abs/1906.08237)

* 文章使用的圖片截圖自論文

如果你喜歡我的文章，可以捐贈我一杯[大熱美（大杯美式咖啡）](https://www.buymeacoffee.com/theblackcat102)支持我。

