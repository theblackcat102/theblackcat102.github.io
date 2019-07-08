---
keywords:
  - NLP
  - n-grams
  - language model
  - brown clustering
comments: true
title: Brown clustering, a class based n-grams model
---

Projecting word to high dimensional space (word2vec) has been a normal practice in NLP domain. The most common algorithm used are continuous bag of word (CBOW) and skip-gram.

[Brown clustering](https://www.aclweb.org/anthology/J92-4003) is another variant of n-gram model. It works by assigning each word to one type of class to maximize the joint probability of all words within a sentence, hence the name of the paper : Class-based n-gram model of natural language. In the paper, the author only shows the equation for class based 2-gram model, but it should be trivial to scale this to 3-gram models.

The definitions are as follows:

$$
\begin{align}
V = {w_{1}, w_{2},...,w{T}} \\
C(w_{i}) = k, k \in {1,..., N}, t >> N\\
\end{align}
$$

* V the vocabulary sets

* Function C will assign each word to a class k, where the number of classes are smaller than the vocabulary set.

Function $$C$$ must maximize the join probability ( $$p(w_{1},...,w_{m})$$ ) of a given sentence of words $$w_{1}...w_{m}$$

$$
\begin{align}
    p(w_{1},w_{2},..,w_{m} ) = \prod_{i=1}^m e(w_{i}|C(w_{i})) \times q(C(w_{i}|C(w_{i-1}))\\
    e(w_{i}|C(w_{i})) = \frac{count(w_{i})}{ \sum count(w_{k,  C(w_{k}) = C(w_{i})}), }\\    
    q(C(w_{i})|C(w_{k})) = \frac{count(C(w_{k}),C(w_{i}))}{count(C(w_{k}))}\\
\end{align}
$$

For example given a vocabulary with the set as follows

| word    | frequency |
| ------- | ---- |
| the     | 4    |
| a       | 2    |
| dog     | 3    |
| cat     | 3    |
| runs    | 3    |
| jumps   | 3    |

Example 1 : $$C(the) = C(dog) = 1, C(a) = C(cat) = 2, C(runs) = C(jumps) = 3$$

$$
\begin{align}
p(the, dog, runs) &= e(the | C(the))\times q(C(the)|C(w_{0})) \times e(dog | C(dog)) \times q(C(dog)|C(the)) \times e(runs | C(runs)) \times q(C(runs)|C(dog))\\
&= \frac{4}{7} \times \frac{4}{6} \times \frac{3}{7} \times \frac{2}{7} \times \frac{1}{2} \times \frac{1}{2}\\
&= \frac{4}{343}\\
\end{align}                        
$$

Example 2 : $$C(the) = C(a) = 1, C(dog) = C(cat) = 2, C(runs) = C(jumps) = 3$$

$$
\begin{align}
p(the, dog, runs) &= e(the | C(the))\times q(C(the)|C(w_{0})) \times e(dog | C(dog)) \times q(C(dog)|C(the)) \times e(runs | C(runs)) \times q(C(runs)|C(dog))\\
&= \frac{2}{3} \times \frac{6}{6} \times \frac{1}{2} \times \frac{6}{6} \times \frac{1}{2} \times \frac{6}{6}\\
&= \frac{1}{6}\\
\end{align}
$$

Noted that $$w_{0}$$ also assigned to a count value of 1.

As we can see if dog, cat and a, the assigned to the same class, the joint probability of the sentence will be larger. Semantically, the function $$C$$ will learn to cluster similar words into the same class. Brown clustering solve some of the n-gram problem which is each word are only assigned to one probability distribution, synonyms cannot be represented under n-gram. However, using brown clustering with a very high class number (N=1000) would require $$V^3 $$ to compute (as compare to the naive approach of $$V^5$$). 

## Advantage to n-grams model

* lesser parameters

Since n-grams model treats each word as an independent class, the required parameters will be enormous. As the n increases the frequencies of n-grams that do not exists in the running set will increase, which can be seen as a waste of parameters. Hence brown clustering assign each word to a class $$c_{i}$$ where $$i < K << V$$, significantly reduce to one third of the parameters required to represent the same n-grams model.

* semantic clusters

```
we our us ourselves ours
question questions asking answer answers answering performance performed perform performs performing tie jacket suit
write writes writing written wrote pen
morning noon evening night nights midnight bed attorney counsel trial court judge
problems problem solution solve analyzed solved solving letter addressed enclosed letters correspondence large size small larger smaller
operations operations operating operate operated school classroom teaching grade math
published publication author publish writer titled wall ceiling walls enclosure roof
sell buy selling buying sold
```
Some words from the same class (Table 6 from [Brown et al](https://www.aclweb.org/anthology/J92-4003))

Brown clustering was shown to cluster words with the same morphological stem, such as publish, publication, published to the same cluster. Some cluster also contain words with similar semantic meaning such as morning, noon, evening, night, midnight. 
