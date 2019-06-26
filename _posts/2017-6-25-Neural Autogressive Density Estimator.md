類神經網路自回歸密度估計 Neural Autoregressive Density Estimation (測試中)


[]()
[Hugo Larochelle 演講的 Slide ](http://helper.ipam.ucla.edu/publications/gss2012/gss2012_10616.pdf)

在機器學習領域中如果想要找出數據的機率分布密度函數 ( probability density function PDF )，一般上用的是 Auto encoder, restricted boltzman machine (RBM ) , GMM。然而另一個比較少人知道的方法是 NADE 也就是利用自回歸來找出數據的 PDF。NADE 在實驗中證明比RBM, Auto encoder 來的更加優秀，尤其超越了伯努力分佈一直非常有效 RBM 。

NADE 認為一個高維度的輸入，第 N 維度的值可以表達成一個前 N-1 維輸入的因式分解函數。

$$
p(x) = \prod_{k=1}^D p(x_{k} | x_{ < k } )
$$ 

作者在其中一個演講中提到，即使數據的各個維度沒有前後順序關係這樣的公式依然可以套用 。（https://www.youtube.com/watch?v=R8fx2b8Asg0）

為此作者提出我們可以學習一個共同使用的權重用以產生一個 latent space $$h_{x}$$ 並用它來生成出輸入 $$x$$。 整個模型的公式如下：

$$p(x_{o_{d}} = 1 | x_{o_{<d}} ) = act(V_{o_d}*h_{d} + b_{o_{d}} )$$
$$h_{d} = act(W_{o_d}*x_{<d} + c )$$

其中 V, W, c, b 都是可以透過 SGD 學習的權重。而全部 $$x$$ 共用同一群權重，作者表示共用權重比起 VAE 更加難 overfit 在不需要 regularization 下也可以訓練好。