---
keywords:
  - dropout
  - targeted dropout
  - deep learning
  - neural network
  - 類神經網路
comments: true
---
Dropout 作為廣泛被使用來防止類神經網路過度擬合 (ovefitting) 的一種機制，在許多大型的類神經模型都會被用到。一般的 dropout 在訓練過程中，隨機將部分的類神經網路屏蔽掉，迫使參數變少後的模型能學習到目標任務。

這篇論文的作者認為過去防止過度擬合的機制偏好使用簡單的估計機制如訓練隨機關掉權重影響、去除最小的權重、根據每個權重對輸入的敏感度排序來修剪類神經網路以達到防止過度擬合的效果。

使用 dropout 的效果是類神經網路會變得稀疏（類神經網路的矩陣中會出現許多稀疏矩陣）。作者認為在訓練過程中與其隨機關掉某些權重，不如根據某些指標來決定關掉一些不重要的權重值。

傳統 dropout 作法有兩種，Unit dropout $$Y = (X \cdotp M) W$$ 與 weight dropout $$Y = X ( W\cdotp M)$$ 。$$M$$ 為一個稀疏矩陣，也就是負責完成 Dropout 功能。

Unit dropout 是將部分的輸入關掉（矩陣的某些值變 0），避免類神經過度依賴某些輸入參數，達到防止過度擬合。而weight dropout 則降低類神經層與層之間的某些連結過度依賴的情況發生。 這兩者比較常見也最常用到的是 Unit Dropout。

### 根據輸入大小值來做 Dropout

作者提出一個簡單的排序機制來決定要保留哪些權重。

1. Unit pruning ： 根據 $$L^2 norm$$ 最大的前K個權重
    $$W(\theta) = \left \{  argmaxk_{1 \leq o \leq N_{col}(W)}  \left\lVert w_{o} \right\lVert_{2} |  W \in \theta \right \}$$
    
2. Weight pruning : 根據 $$L^1-norm$$ 最大的前K個權重

$$W(\theta) = \left \{  argmaxk_{1 \leq i \leq  N_{col}(W)} |W_{io}| | 1\leq o \leq N_{col} , W \in \theta \right \}$$ 

作者有提到一個點是 weight pruning 可以在最大程度上保留模型的最大表現，而unit pruning 則是提升運算效能。

### 結果：

為了評估效果，作者使用 Resnet 32層模型，在CIFAR-10 資料上比較不同程度的 Dropout 與不同機制下的結果。這裡應該比較注意的是將 $$$$$$n \%$$ 的屏蔽掉後的準確度。可以看到 targeted 的 Dropout 即使在 80% 的權重被屏蔽以後，準確率最高還可以到 92%。而Unit Dropout 在屏蔽 50% 的輸入值以後，準確率最高還有80%。
  

![](https://paper-attachments.dropbox.com/s_BDBF10E8BE10AD207C217D0D6C011B55E08FE56FF8956EB491C08FBD604E41AE_1561912048467_Screen+Shot+2019-07-01+at+12.25.10+AM.png)


\[原論文連結](https://arxiv.org/abs/1905.13678)
作者 ： Geoffrey E. Hinton, Ivan Zhang, Kevin Swersky, Yarin Gal, Aidan N. Gomez
