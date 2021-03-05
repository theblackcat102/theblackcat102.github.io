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

hyponymy : 下位詞，與詞彙相同層級的其他詞彙，例如 牛、羊、狗 都是脊椎動物的下位詞。所以脊椎動物的下位詞是牛、猴... 

hypernym : 上位詞，下位詞反向意思，例如狗的上位詞是脊椎動物

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


function words : 功能字，如果去掉以後還是不影響句子的意義。例如 : a, the, these 

stop list : 也稱作 stop words, 去掉以後介系詞子句就消失

entailments: 蘊含，一般上是考慮兩個句子 A, B 假設已知A 為真，那接續後面的 B 必須也是真的。例如: A： Jojo 吃了一些蛋糕, B：Jojo 吃了寫東西

implicature: 暗示、話中話。例如： Jojo 吃了一些蛋糕，話中話可以是 Jojo 沒有把蛋糕吃完

presupposition: 前設，表達給定一個句子，任何前設句都是該句子可以成立先決條件。例如 Jojo 吃了蛋糕，前設：有一個蛋糕。

adpositions: 介詞，一般上是指所有介詞的名稱。介詞被使用在連結兩個概念之間的關係。例如前面的“介詞被使用...” 裡的 "被" 就是介詞

prepositions: 前置介詞

postposition: 後置介詞

cirsumposition: 框式介詞

relativizers ： relativizers （中文沒有特別名詞表達這意思？）用於代替被指定的人、事、物。例如 who is the president? 中 who 就是  relativizers 一種。常見的 relativizers 有 : which, where, who, whom, whose, when, how, that, this ... 

collocations : words that exist in the same context, their relations doesn't need to be in the neighbour (can be far a part)

concordances : given any words, you can find a sets of strings which can be placed in front and back of the words ([COCA](https://www.english-corpora.org/coca/))


