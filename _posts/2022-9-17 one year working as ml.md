---
keywords:
  - experience
comments: true
title: 電機轉軟體工作一年的心得
cover_image: https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/275454762_664831364726776_7634964100785791094_n.jpg
---

不知不覺就在小公司待了滿一年，相比同屆去上市公司/外商我算是異類中的異類。雖然工作就是工作也沒什麼好拿出來說的，但是我覺得在大家都在說跳外商或豬屎屋（ IC design house ) 多好的時候，我就想出來亂一下。

![Attention coffee](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/275454762_664831364726776_7634964100785791094_n.jpg)

> I dont really like talking about myself either. And most of these things here I don't really talk about myself.
> I do give anecdotes of my life but they're more to illustrate a point. Because anything about myself is useless to you. 
> Do be like me, that's dumb. I try to give you information so you can think - George Hotz

關於我的背景：大學來台灣唸書6年（交大電機碩士），成績不怎麼樣，但是寫寫程式還行的普通人。目前在小公司擔任機器學習工程師

以前我在軟體實習的時候就感覺我是一個坐不住的人。用中文來說就是我無法長久專注，遇到我感興趣的問題就會沒日沒夜去找出 solution，大概3-6個月就會失去興趣。所以我的 side projects各種成長，但是沒幾個能持續維護的。因此在實習以後我就覺得我應該不會適合去大公司做企業印鈔器中的奈米螺絲。~~我就不想一天就寫一個 function 打卡下班~~

因此實習到一半其實我就做不下去提早結束實習，開始我的技能樹展開生活。大學從 android app、農委會計畫當程式打手、寫網頁前後端並搭上ML/AI崛起的熱潮，變成如今在 “AI” ~~騙吃騙喝~~ 做關於文字理解 & 處理、影像處理、推薦相關的商業應用，偶爾[實作 paper](https://github.com/theblackcat102/language-models-are-knowledge-graphs-pytorch)打臉人。然後2021年碩士電機畢業。


> 啊，2021年的電機系畢業，應該過得很好吧？


> Nope， 因為我去了軟體業


## 台灣軟體業

1. 台灣軟體業心酸

**蛤，軟體不是科技業啊**

畢業的時候剛好遇到竹科大徵才時代的最後一波，因此同屆的朋友隨便面試都可以到年薪 > 120萬的級距（這是排除我後的低標），對我形成不小的壓力。但好在工作半年後升遷拿到了約竹科2022年二線水平的待遇。

2. 在薪資上，年資 > 實力??

**“我有5年經驗，所以我值得 N ”**

因為有幸獲得上司青睞，所以參加了幾場新人面試，我發現一個事實是舒適圈的可怕。有一次面試到一位竹科10幾年經驗的工程師（做內部雲服務），在面試時連簡單考的邏輯程式都寫不好（不是 leetcode 類題目），但是因為其他項目表現不錯於是讓他入取了。報到1個月後發現各個項目真的很茫，於是就還未滿3個月就走了。

那時候我其實在想，會不會以後我自己也會變成他那樣。尤其是在迭代速度如此快的 AI 領域，做一做就變成新鮮人眼中的老人了。


2. 台灣沒有 AI

其實這論述不能說錯，但也絕對不是沒有。至少從近年開始有外商公司將演算法部門設立在台灣來看就知道其實台灣是有 AI 人才，只是靠AI圈錢的公司還是太多。

但我自己認為深根AI技術的公司（例如 kakao brain, deepmind, 阿里達摩學院 這類）在2022年是不存在的。多數還是以商業問題為導向，看什麼行業火熱就發發新聞稿說自己導入AI~~圈錢/炒股~~ 

但反思這個問題的根本其實還有雞生蛋 or 蛋生雞的問題。雞可以看成AI深根，蛋就如人才/資本。如果在台灣AI最厲害人才的都去竹科工作那自然就不會有人在解決，而竹科因為成本競爭與文化因素，一般也不會做得太深入，反而選擇跟著領頭羊做到參數匹配但便宜就好。當然問題背後還有人才流失的問題、學界當RD部門用、市場規模 etc 等等因素。而我只是想吐槽當大家都去竹科，在軟體業的 AI 當然就剩下...

有興趣可以看看這本書[《人工智慧在台灣：產業轉型的契機與挑戰》](https://www.books.com.tw/products/E050049609)，作者在玉山那段時間的改革蠻有名的

## 收穫

1. weights(溝通) == weights(實力)

**尤其是面對同溫層以外的人，有良好的溝通能力其實和技術實力一樣重要**

我在工作第一次跨部門的溝通時就被我上司狠狠打槍，指出我的投影片太難理解。並且要求我退回再製作新的投影片。原因是我太習慣與同領域的朋友溝通，所以很多我習以為然的事務其實對於他們來說很難理解 (例如 F1-score)。

2. 不侷限自己

**career think out of the box**

因為公司關係有機會與[簡立峰](https://zh.m.wikipedia.org/zh-tw/%E7%B0%A1%E7%AB%8B%E5%B3%B0)進行一對一聊天。過程中他給了我一個職涯建議，那是將自己定位為：能解決問題的工程師。不需要把自己侷限在 ML/AI 的問題上。這裡解決的問題可能是：資源分配問題、演算法問題、程式優化，而不再是只是ML建模而已。

這其實與 Taboola的 [Algorithm Engineer](https://web.archive.org/web/20220917102253/https://www.104.com.tw/job/7b8t3)理念滿相似的（沒有業配），雖然他們需要 ML 領域的人，但是也要會 DS (如何發掘資料 insight並呈現出來) 、DA (分析資料)。因為它們都是解決問題的一環。

或是如 [mosky](http://mosky.tw)是一個解決問題的工程師，從backend到[線型代數](https://speakerdeck.com/mosky/data-science-with-python)的generalist

3. 軟體業是個海納百川的環境

相較於竹科的公司分工明確，在小公司其實可以遇到很多不同領域/背景的同事。雖然過程中會有不少的摩擦，但是你會看到更多同溫層以外的人，像是我的 team 就有來自森林、應數、統計、金融、管科、新創大神等背景的人。

## 結語

在台灣大家都覺得AI待遇真的很爛，所以我有機會建立公司的AI基礎（雖然多數還是屬於胡搞瞎搞），作為累積眼界廣度的一種切入點。往好的方面想就是係上的大神都跑去SV或竹科工作了，潛在競爭者都離開這鬼島了。

But, 前提是你要遇到好的老闆

如果你是外籍人士：維持你的英語言能力，文件、筆記能用英文就英文。維持/增進實力以隨時跳槽其他國家的準備

## AI 勘誤

#### AI都是模型套件仔

幾年前可能會看到一堆在酸說 “AI 不就是模型套一套就好了嗎？”。我覺得到了2022年，尤其景氣下滑的背景下，單會 keras 去 fit 模型應該是快混不下去了。我不敢說台灣不會有公司會收你，但如果面試遇到我你會過不了我這關。

至少在我工作上，我就需要寫新的 objective function/loss 去改善問題、調整模型架構讓它能滿足計算資源與預測效能的要求、從0開始解決一個學界沒有的問題（paper 找不到，但是有相似的問題）。與其說 AI 是套件仔，不如說是 paper 實作員

![How to be a machine learning engineer](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/geohotz_how_to_become_programmer.png#center)



