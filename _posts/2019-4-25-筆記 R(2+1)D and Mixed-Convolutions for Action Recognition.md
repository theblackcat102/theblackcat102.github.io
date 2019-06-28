---
keywords:
  - deep learning
  - neural network
  - 卷積類神經
  - R3D  
  - 深度學習
---

使用 Convolution 有效學習圖片+時間資訊: R(2+1)D and Mixed-Convolutions for Action Recognition

[網址](https://arxiv.org/pdf/1711.11248.pdf)

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/r3d.png#left)

過去 Action recognition 可以透過單張圖片進行classification 就達到非常接近 State of the art 分數 。因此作者嘗試加入 3D 卷積層 ( conv ) 使得model 具有時間學習能力。為了降低參數量，作者分別提出了混合 conv 與 R2+1 conv 模型。前者在input 前幾層使用 3D conv 做encoding 再轉為 2D conv，後者則是一個使用兩個 3D conv 來分別表達圖片與時間的訊號。這個2+1 的conv 結果準確率顯示遠勝於混合 conv 與 3D conv 模型。



右圖顯示 R2+1 conv 第一層先在M個不同時序上做 dxd kernel 的卷積，接著再通過一個 t x 1 x 1 的 3D 卷積。這樣的設計除了降低參數量之外還可以在中間加入激活層或是 normalization 層。

後記：是否能應用在LipNet 解讀嘴唇話語？畢竟模型需要理解時間、嘴唇熱點之間的關聯。


如果你喜歡我的文章或side projects，可以捐贈我一杯[大熱美（大杯美式咖啡）](https://www.buymeacoffee.com/theblackcat102)支持我。