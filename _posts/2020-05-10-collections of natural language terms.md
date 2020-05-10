---
keywords:
    - NLP
comments: true
title: 自然語言專有名詞對照表
---

說實在的因為小時候英文學不夠好，結果目前在看自然語言處理的 paper 總是遇到很多每次都要查的專有名詞（有時候自己會有股衝動去修外文系的語言學 .... ）。所以有了這篇專有名詞對照表。

一下內容是根據我自己對於英文解釋的理解翻譯來的中文解釋，如果有錯誤請留言跟我說 QAQ

(不定時更新)

phrases semantics : 短語語意

predicates : 謂詞，提供主語資訊的部分

syntax ： 語法

polysemy : 一詞多義

content words: 泛指能對句子的語意做出貢獻的字，一般上是名詞、形容詞、副詞。與之相反的是 function words 則是方位詞、代名詞

lemmatization : 詞形還原，就是將字還原回原本的型態。例如過去詞變成現在詞, drove 變成 drive。

stemming : 詞幹提取，顧名思義就是提取詞彙的主幹字段。例如 dogs 的詞幹就是 dog, revival 是 reviv。詞幹提取雖然能降低語料中詞彙的數目，但也會引入新的且不存在詞彙（revival 變成 reviv）

valency : 在語言學中早期會針對形容詞的特性依照他們在句子中依賴的總對象做分類，例如 give 的 valency 為 3 ( I give you this apple, give 依賴 I, you, apple )。相同的價位(valency)的字理應上就會有出現在句子中相同的位置，與化學的價電子很相似。

part of speech : 詞類，一般常見的名詞、動詞、形容詞就是屬於詞類

entity : 實體，指句子中能對應到現實世界中實體人事物的字，例如人名、地名

constituency tree :  constituency tree 為語言分析樹的一種。它只有三種 node ： root,  branch, leaf node。其中 root node 為整個樹根的起點，branch node 用於表達子節點之間關係（phrasal categories ） ，leaf node 則是表示句子中每個字對應的詞性（名詞、形容詞..）。


                     Sentence
                         |
           +-------------+------------+
           |                          |
      Noun Phrase                Verb Phrase
           |                          |
         John                 +-------+--------+
                              |                |
                            Verb          Noun Phrase
                              |                |
                            sees              Jane

dependency tree : 相比 constituency tree, dependency tree 只有規劃出字之間的關係，每個節點直接對應句子間的詞性。

                  sees (V)
                    |
            +--------------+
            |              |
          John(N)         Jane (N)

範例來自https://stackoverflow.com/questions/10401076/difference-between-constituency-parser-and-dependency-parser

