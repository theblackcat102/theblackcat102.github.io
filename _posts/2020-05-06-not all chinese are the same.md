---
keywords:
    - NLP
    - Chinese
comments: true
title: Not all Chinese are the same
---

For many non Chinese speaker, these sentences may appear same to you.

```
可以不可以做很多的但是不用洗锅的甜品
可以不可以做很多但是不用洗鍋的甜品
可吾可以整多啲吾洗焗嘅甜品
```

Yes?

Well, technically they share the same meaning but are presented in three different Chinese "language"*.

```
simplfied chinese : 可以不可以做很大份但是不用洗[锅]子的甜品
traditional chinese : 可以不可以做份量多但是不用洗[鍋]的甜品
traditional chinese in cantonese : 可吾可以整多啲吾洗[焗]嘅甜品
```

* Note the bracket characters point to the same meaning : pot but use different character representation.


Simplified chinese are commonly used in China, Malaysia, Singapore while traditional chinese font is widely adopted in Hong Kong, Macau, Taiwan with small users in south east asia printings.

Although they all share the same Hieroglyphic characteristic, the words (not character) are different across different regions.

|English | China | Hong Kong, Macau | Taiwan | Malaysia, Singapore |
|------------|---------------|--------|------|------|
| Tie |領帶	| 領呔、呔	 | 領帶	 | 領帶|
| Trench Coat| 風衣	| 風褸	 | 風衣	|
| Rain coat | 風雨衣	| 乾濕褸	| 風雨衣	|
| Sweater | 毛衣	| 冷衫	| 毛衣	| 冷衣|

They way they type in chinese are also different, for example Malaysia, Singapore usually type in a Chinese/English/Malay twish of Chinese ( google Singlish ). Other chinese speaker from the other 3 regions will not understand the meaning without an 101 introduction course. The same goes for Taiwan which usually contain a mix of Minnan language and Chinese. While Hong Kong, Macau is typing in Cantonese is an either different grammar rule than Chinese. 

However, in the domain of NLP, these language are assumed to share the same grammar and syntax rule but in reality they are different. Even most common language detection task fail to address this problem, and simply assume these "characters" are the same language. In a sense this is similar to a person assuming Malay and English are the same since they use the same alphabet system for word representation.

```
Malay: Apa khabar
English: Hello
```

Yeah, they looks the same...

There's a ton of NLP research in Simplified Chinese, these results are usually bad when transfer to another one. For example, the popular chinese segmentation tool [jieba](https://github.com/fxsjy/jieba) works quite well in Simplified Chinese but not so when you try to use it in Traditional Chinese due to the difference in word distribution. [jieba-TW](https://github.com/ldkrsi/jieba-zh_TW) is a port of jieba which specifically sampled from Traditional Chinese in Taiwan.

I think there's more work to be done to address the difference of Chinese language from different regions, especially Cantonese. 

