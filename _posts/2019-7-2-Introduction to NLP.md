---
keywords:
  - NLP
  - 自然語言
  - deep learning
  - neural network
  - 類神經網路
comments: true
title: 自然語言從古至今 Part 1
---

在自然語言領域 (NLP) 做了十幾年的[韓國教授 Seung won Hwang](https://www.semanticscholar.org/author/Seung-won-Hwang/1716415) 受邀來交大給2個關於 NLP 的演講。演講大概就是分享近年 NLP 的進展程度與NLP常見的任務種類。

第二天會談談在有限資源下運用知識圖來突破這些限制。

這兩篇文章會大致寫寫講座內容，過於零散的內容我就不說了。

# Introduction 語言模型的類型

根據不同的任務，我們可以將它們表達為不同的機率函數。

    - Language model LM:  $$p(text)$$
        - 生成順暢且正確的句子
        - How to generate fluent and grammatically correct text?
        - 需要具有 Common sense （理智）如： The store went to Jane. 
    - sequence to sequence (seq2seq) 給定一個句子輸出句子 : $$p(text | text)$$
    - 自然語言分類或回歸任務 : $$p(label| text)$$
    - 生成知識譜 $$P(graph\ or\ tree | text)$$


# 深度學習前的自然語言：

1. *(1992) n-gram*
    根據詞頻作為該文字的機率函數，然而 n gram 的問題有：前期統計沒有出現的字模型無法處理（也就是常見的 Out-Of-Vocabulary OOV 的問題）、無法抓取句子前後詞的關聯（n 值一般 < 5）,同義詞一般會被考慮為一樣的字（統計時前後出現的詞類似）。
    舉例 bi-gram (n=2) 模型如下：
        $$
            p(w_{2} | w_{1}) = \frac{count( w_{1}, w_{2} )}{count(w_{1})}
        $$

2. *2013 文字向量 word2vec: bag-of-word(BOW, skip-gram*
    2013 年提出了將詞轉向量的概念，每個詞被指定到一個高維度的向量空間，並透過 BOW 或 Skip-gram 學習每個詞所對應的向量空間。

    CBOW: 透過一個移動窗口( $$w_{C}$$, $$w_{C+1}$$,...,, $$w_{C+N-1}$$, $$w_{C+N}$$)，學習預測中間的詞 $$w_{C+\frac{N}{2}}$$

    Skip-gram: 透過中間的詞預測前後可能出現的C個詞

    ![](https://www.researchgate.net/profile/Wang_Ling/publication/281812760/figure/fig1/AS:613966665486361@1523392468791/Illustration-of-the-Skip-gram-and-Continuous-Bag-of-Word-CBOW-models.png)

    相比 ngram, word2vec可以學習相似的字會有相似的鄰居字，因此投影出來的  word vector 能表達某種“知識向量”，如  King - Queen = Boy - Girl ( 兩性差異）
 
    目前許多state of the art (SOTA) 的模型(BERT, GPT, MASS, XLNet) 基於詞、句空間的概念，提出如何學習含有更抽象的語意、語法的向量空間。

# 將句子表達為向量 (vector)

如果詞向量表現那麼好，那可以學習句/文向量嗎？

```

"You can’t cram the meaning of a whole %&!$ing sentence into a single $&!*ing vector!"
  - Ray Mooney

```

從過去的論文中（忘了哪篇了，之後想起再補上），只要sentence vector 的維度越大，表現結果更好。如果說一個 vector 不夠那可以動態的讀取數個 sentence vector 來表達文本含義呢？

答案：用隱藏向量的 weighted sum 作為 sentence vector ，也就是常見的 attention 機制。

[兩種不同的Attention機制](http://cnyah.com/2017/08/01/attention-variants/attention-mechanisms.png
)

![](https://paper.dropbox.com/ep/redirect/image?url=http%3A%2F%2Fcnyah.com%2F2017%2F08%2F01%2Fattention-variants%2Fattention-mechanisms.png&hmac=JQq5ruQKFQx0jsjVwS8%2FitGYGTq7QpiGS27RN39lIWY%3D)

# 時間到

受邀教授說到這裡時間就差不多結束了，下一部分（隔天）會講解NLP 目前的一些問題跟缺口。

因為開頭說了很多關於知識圖（ knowledge graph ）的介紹，我就問了教授會不會談談最近發表：結合語言模型 (LM)與知識圖(KG) 的 ERNIE（ERNIE 有兩篇，一篇清華另一篇是百度）。韓國教授就說盡力這樣。(沒辦法我們都是比較內向的人把，這談話就尷尬的結束了...）


