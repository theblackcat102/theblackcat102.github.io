---
keywords:
  - deep learning
  - neural network
  - skip connection
  - 深度學習
---

這年頭時不時都來一個 skip connection, 認為此風不可長的研究員就想出了 FractalNet。基於Skip connection 解決vanishing gradient 問題的理念，Fractal Net 使用梯子設計形式，增加信息可以流向的pipeline 。由於每個 pipline 所經過的權重比較少，因此 gradient 可以透過比較沒有什麼阻抗的 pipeline 更新比較底層的權重。

每個pipeline 所經過的卷積層 （ conv → batchnorm → relu ）最多兩層就與鄰居pipeline concat 或 add ( 統稱 join )起來了。這樣的設計定為一個 block, 每個block 之間做池化。每個階梯層的分離與結合稱作 path，在最後的join 層它可以結合深淺度的特徵。而整個網路中完全不依賴任何的skip connection 結構，也達到了超深的類神經網路結構

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/fractal.png)

這樣的設計可以在不使用data augmentation情況下，超越 resnet 。此外，因為Drop path 可以將部分的資訊修剪，因此更加robust。

Regularization method: 為了訓練如此龐大的網路，在訓練時每個路徑都會隨機被 drop, 這包括全域與小區域的 drop, 例如上圖在 Input 分成了 4 個 channel, 全域 drop 就是其中一個 channel 被停掉，小區域則是大 channel 下被切分的channel。

作者在最後結語說為何這樣的設計有 student teacher 形式的關鍵在使用 drop path 。假設 channel 3 是比 4 深, 當 channel 3 被丟棄時，channel 4 被迫分擔 3 的工作。作者將部分的 channel 提出組合成新的模型，它依然能正常運作（沒說準確率降低多少）。

問題： 記憶體佔用，如此之大的模型其 channel 必然導致記憶體佔用量提升。這也許是為什麼作者只有做到 40 層的緣故。

如果你喜歡我的文章或side projects，可以捐贈我一杯[大熱美（大杯美式咖啡）](https://www.buymeacoffee.com/theblackcat102)支持我。