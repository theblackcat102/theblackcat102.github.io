# 類神經網路自回歸密度估計 Neural Autoregressive Density Estimation

### 介紹 NADE 基本架構

在機器學習領域中如果想要找出數據的機率分布密度函數 ( probability density function PDF )，一般上用的是 Auto encoder, restricted boltzman machine (RBM ) , GMM。然而另一個比較少人知道的方法是 NADE 也就是利用自回歸來找出數據的 PDF。NADE 在實驗中證明比RBM, Auto encoder 來的更加優秀，尤其超越了伯努力分佈一直非常有效 RBM 。

NADE 認為一個高維度的輸入，第 N 維度的值可以表達成一個前 N-1 維輸入的因式分解函數。

$$
p(x) = \prod_{k=1}^D p(x_{k} | x_{ < k } )
$$ 

作者在其中一個演講中提到，即使數據的各個維度沒有前後順序關係這樣的公式依然可以套用 。（https://www.youtube.com/watch?v=R8fx2b8Asg0）

為此作者提出我們可以學習一個共同使用的權重用以產生一個 latent space $$h_{x}$$ 並用它來生成出輸入 $$x$$。 使用 SGD 訓練則以降低 negative log probability 來訓練。整個模型的公式如下：

$$
p(x_{o_{d}} = 1 | x_{o_{<d}} ) = act(V_{o_d}*h_{d} + b_{o_{d}} )
$$


$$
h_{d} = act(W_{o_d}*x_{<d} + c )
$$

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/NADE-1.png#left)

其中 $$V_{o_d}$$, $$W_{o_d}$$, $$c$$, $$b_{o_{d}}$$ 都是可以透過 SGD 學習的權重。$$W_{o_d}$$ 為 D x H 維度的矩陣，且每一個順序 $$x_{d}$$ 僅僅對應到一個 $$w_d$$ 向量。如圖中所示生成每個隱藏向量 $$h$$ 的箭頭顏色對應到一個 $$w$$ 權重。同樣 $$V$$ 向量也是與$$W$$一樣。

在訓練的過程中，維度的順序會隨機生成(orderless)，意思是每個維度的值的自回歸順序可能是 0 -> 1 -> 3 -> 5 -> 4 -> 2 或 5 -> 1 -> 2 -> 4 -> 3 。此外 NADE 也可以同時訓練多個不同的隨機順序來做提督下降。[[程式示意]](https://github.com/MarcCote/NADE/blob/master/deepnade/buml/NADE/OrderlessBernoulliNADE.py#L124)


由於全部輸入 $$x_{d}$$ 共用同一群權重，[作者表示](https://youtu.be/R8fx2b8Asg0)這樣的機制比起 VAE 更加難 overfit 在不需要 regularization 下也可以訓練好。但是我認為NADE會比VAE更好應該是來自將因式分解以自回歸求解的機制而不關權重共享的事，因為 MADE 的模型利用 VAE 架構 + Mask 


### NADE 變形

基於以上的概念，我們可以衍生成不同的架構如輸出為實數的 RealNADE、適合用於圖像的 ConvNADE、多層隱藏空間的 DeepNADE、用來取樣Laplace 分布的 LaplaceNADE 。

其中 RealNADE 與 LaplaceNADE 相似，都是將每個輸出對應到一種參數不同但同類的機率分佈函數權重（例如不同平均、標準差的高斯分佈）。透過相同的訓練方式學習到某實數的機率函數。

## 衍生閱讀：

* [ArXiv NADE 論文網址](https://arxiv.org/abs/1605.02226)

* [code 實作DocNADE](http://blog.aylien.com/tensorflow-implementation-neural-autoregressive-topic-model-docnade/)

* [Hugo Larochelle Youtube 演講](https://www.youtube.com/watch?v=R8fx2b8Asg0)

* [Hugo Larochelle 演講的 Slide ](http://helper.ipam.ucla.edu/publications/gss2012/gss2012_10616.pdf)
