---
keywords:
    - large language model
    - llama
    - open source
    - thoughts
comments: true
title: Short writeup of "Unpopular opinions on AI"
---

"Unpopular opinions on AI" is a podcast episode by ZhenFund team thoughts on LLM at a sharing in China in simplfied chinese with [Peak Ji](https://www.forbes.com/sites/russellflannery/2013/03/19/forbes-china-30-under-30-list-ji-yichaos-mammoth-ambitions/?sh=75076c5c3483)

<p align="center">
<img src="https://github.com/theblackcat102/theblackcat102.github.io/blob/master/images/df80a7555e4242ce8e7b5b0457bb9fb5.png?raw=true" height=300 stylesheet="center">
</p>


Podcast episode : [特别放送：一个 AI 创业者的反思、观察和预测](https://podcasts.apple.com/tw/podcast/%E7%89%B9%E5%88%AB%E6%94%BE%E9%80%81-%E4%B8%80%E4%B8%AA-ai-%E5%88%9B%E4%B8%9A%E8%80%85%E7%9A%84%E5%8F%8D%E6%80%9D-%E8%A7%82%E5%AF%9F%E5%92%8C%E9%A2%84%E6%B5%8B/id1689996400?i=1000617571314&l=en)

Original transcript in chinese can be found [here](https://www.facebook.com/hinet/posts/pfbid02E5rWmzuFWHpNiXDf2co14EDDeKVtY24StU4GUm4msDoY3kkP9pRQUgpf3SnPAEsjl)

I am not going to just do a english translation of this posts, you can copy and paste the entire post transcript into GPT-4 and it should give you a reasonable translated article. This article is about a short writeup on the interesting parts and some thoughts of mine.

The entire posts is quite long even in chinese, but they basically discussed these ideas which I find pretty interesting.

1. What's the valuable part in this LLM trend?

2. Seeing the LLM from the founder and investor perspective

3. Some predictions by the speaker

These are also some of the questions I have been asking myself since the start of chatGPT phase

## 1. What's the valuable part in this LLM trend?

Basically there's 3 parts the term valuable can be defined or viewed from:

### We are all equal

Similar to the early phase of iPhone apps store where the most popular apps are still farts app or flashlight. Productivity apps would not emerge until a few years later. As of June 2023, we are still in the farts app in LLM applications (fart phase). 

So for startups we are actually on the same starting point as the giants on the application side. Such as a rewind.ai like service running on your smartphone offline. Meaning your phone runs a "small" LLM which aggregates and answer all the questions you had in your phone. Or on-perm service using special accelerators such as MLU370 and M100 (not Mi100). Since there's a need in China to replace certain percentage of your stack to china manufactured hardware, I think this example is only unique in China only.

I find the on-device idea pretty interesting because for one I was training a few [3B chat models](https://huggingface.co/ikala/bloom-zh-3b-chat) few months back and 3B is actually in the range where you can [run it on your iPhone](https://twitter.com/togethercompute/status/1660767722073128960). But for such as "small" model, its bit hard to make use since one of the core of LLM trending cause is that its very versatile, meaning you can use it to do any kinds of things without prior design. But for 3B model, it really can't handle unseen task in my testing, this novel use is only and could only be improved via scaling the weights (3B -> 7B -> 13B). So in order to find any use of turning your iPhone into a hand warmer, there must a killer application for it to exist. For example, your on device LLMs would help you reply chat message or aggregate which apps you should open or use next?

### Data

There's a unique take on what defines data moat here which I find the most interesting and I quote (in slight translation of mine):

> I think from the start of the chatGPT phase, a lot of voices are showing data platform are going to close up their access (Reddit, StackOverflow) to show case their own "unique" data value. But right now even proprietary data which you have collected would not be valuable anymore. 

My personal interpretation of this means any "proprietary" you have collected to train a model would have no value. For example, the labeling and conversation data collected by OpenAI used to train the SFT or reward model phase. In the original article, the speaker refers to data collected in your vertical stack. 

So what's valuable then? Its the data which do not belongs to you. For on-premise deployment example, the solution and the data which was generated via this on-prem is valuable cause it bonds you (the service provider) and the enterprise (customer) together. For example a human feedback pipeline which is closely integrated with the customer stack and the customized module trained on this pipeline (ie LoRA).

### Focus in building relationship with users 

Subsequently after the popularization of LLM, you could now use in context learning prompts to solve any problem. So what's most valuable left is in creating a relationship with your users instead of creating a custom model/service stack to solve the problem. Thats a echo for the data moat problem, which I agrees 100%

## 2. Some predictions by the speaker : context and embedding

Prior to word2vec understanding or query of text relies on building hard mapping of synonyms and antonyms of words. And word2vec would map word into a latent space where thinsg with similar meaning (the mapping) could be learned without supervised (unsupervised). But one problem with word2vec is that it would think Apple (the company) and the fruit are the same since it's learned on a word basis without considering the context. 

After word2vec, we have the next big change which is Elmo, solving the "Apple" problem of word2vec. Its not really popular compared to Elmo because after a year there's BERT which tackles exactly the same problem but way faster due to the parallelism nature of transformer compared to recursive models (Bi-LSTM)

And the next big innovation the speaker thinks would be context size, ie the numbers of tokens your model can handle and still do well. Current method relies on embedding method for long context via retrieve and append to the prompt strategy. But in and my experience, embedding method rarely exceed traditional search method in 90% scenario. Another issue with embedding is the number of information stored vs traditional reverse index method. One trick I saw again and again used to encode long article is a overlapping window method where you only encode few sentences as a embedding and move the sentence window forward until you reach the end of article. This method obviously would generate a large amount of embeddings representation the article, but its currently the most effective method.

## 3. Product managers who really knows ~~AI~~ ML

Building a machine learning product or "AI" central product is very different than "traditional" product. Traditionally, services focus in QPS (query per second) and scalability. But for ML product, especially LLMs product there's really no QPS. And the most important part is how feedback would be built in the product from the 1st day.

Midjourney for example, would generate 4 images for your prompt and the one you choose would be the human preference image which Midjourney could use it to train a better model [(tweet)](https://twitter.com/sergeykarayev/status/1643284067117580288)

But one concerning issue raised by Peak, is with the complexity of LLMs stacking up, the distance between users understanding and technical alignment gap are also going to get wider and wider.

# Closing thoughts

I would like to quote Peak's ending here, cause its really what I think of his previous product [Magi search](https://magi.com): 

> 你覺得你解決了最顯眼的問題作為你的護城河，但其實有些人在用一個包抄你的方法在解決你的問題。對於任何一個技術創業者，絕對不要把最顯眼的 limitation 當成自己唯一的護城河，需要找到除此之外的點。不然會重蹈我的覆轍

Translate by GPT-4

> "You believe that by solving the most conspicuous problems, you have created your moat, but in reality, some people are addressing your issues in a way that outflanks you. For any tech entrepreneur, never treat the most conspicuous limitation as your only moat; you need to find points beyond this. Otherwise, you will repeat my mistakes."

(Canceling my grammarly subscription and hello ChatGPT Plus)

Just a little bit of context, Peak last founding company was Moji, basically they could generate a knowledge graph from a pool of corpus and achieve a near realtime update of the knowledge graph. Solving this requires a lot of NLU technique such as intent understanding, open information extraction, relation extraction etc back when solving NLP or NLU requires a dedicated model design. But as in June 2023, I could do all the same thing with a single prompt using GPT-4 and simply parsed the knowledge graph from the model response. Any prompt engineer could overtake any NLU based service as long as money is not an object.

[Here's one way to do it](https://neo4j.com/developer-blog/chatgpt-4-knowledge-graph-from-video-transcripts/)

This episode really sums up some of my consideration during this period of explosive technical application in LLMs. Embedding based query is cool and I have been using it since 2021 since [CLIP](https://github.com/openai/CLIP), but pure embedding really add alot of hidden technical debt you can't really tackle immediately, hence lengthen your release cycle. Chat based LLMs interface aren't really useful other than programming domain, good luck buying and scrolling a ecommercial website via chat interface. 

What I really think LLMs are really good is aggregate and summarize, and by summarization I don't refer to the traditional point like summarization. But task based summarization for example you could train a LLM to look at bunch of images and tell me what does the overall image represent or give a transcription of podcast and convert it into a readable article. These kind of new data normalization flow is really where LLMs will shine. [Not being sentient](https://news.ycombinator.com/item?id=35300012) or [solving MIT EECS problem](https://flower-nutria-41d.notion.site/No-GPT4-can-t-ace-MIT-b27e6796ab5a48368127a98216c76864)

# Glossary

[word2vec](https://www.kaggle.com/code/pierremegret/gensim-word2vec-tutorial)

[Elmo](https://towardsdatascience.com/elmo-why-its-one-of-the-biggest-advancements-in-nlp-7911161d44be)

