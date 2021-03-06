---
keywords:
  - search engine
comments: true
title: Designing web search for my personal need
---

In 2021, I kept going into the idea of building a search engine ( or tools to organize the information within my bubble ). This tool should support semantic retrieval in terms of text form.

## An overview of current search market

Search engine is mainly dominated by Google. With the rest fighting for the < 10% market.

![2021 search market overview](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/market_share.png#center)

* Bing.com
    
    - duckduckgo and others uses the same index

* qwant.com

    - They index their own index but it's not available in taiwan

* [cliqz.com](https://cliqz.com/en/whycliqz/search-engine)

    - They shutdown in 2021 and [sold to Brave](https://brave.com/brave-search) which is a ad company package under the privacy focus idea (no way I am using it)


* The parallel world

    - And there's the other world where most people doesn't care : baidu.com (and other chinese search engine), naver.com, yandex.com

    - China search engine sucks since they are just heavily [selling weird ads](https://zh.wikipedia.org/wiki/%E7%99%BE%E5%BA%A6%E7%AB%9E%E4%BB%B7%E6%8E%92%E5%90%8D%E4%BA%8B%E4%BB%B6) with no ethical bottom line 


### How do I use google

These are some of the features I consciously use it for:

1. Debugging : basically fuzzy text match on one stackoverflow question

2. Translation : I am a bilingual using both english and chinese to converse with different social group. So I use google to translate from chinese to english or vice versa for certain words.

3. News or past events, but historical ones. I already have my own [news aggregation website](https://todayheadlines.live/) which I tune it from time to time for my own consumption.

4. Exact page search : search for the one website I saw few months/years back which I don't remember the extact title or link ( this usually time consuming thanks to those SEO optimizers out there)


#### How to find quality 

Some list of good website with good content. You genuine know the author spent time on writing a good essay. 

1. gwern.net

2. [吐納商業評論](https://tuna.to), [股癌](https://gooaye.com)

Its unsure how to make sure good quality website can be determine algorithmically but I am certain one of the solutions involve neural networks and the other is distributed crypto chain. Jokes aside, I think a continous stream of data collection is [unavoidable](https://0x65.dev/blog/2019-12-02/is-data-collection-evil.html), as a system without feedback loop simply can't detect a regime shift in user behavior.

#### Coverage != quality

What we search today is only 3% of what the entire searchable internet. Since everyone is just using these small percent of the internet my guess it everyones results would be similar even across different types of index. Which is why i think there might be a opportunity here for small indie search to shine.

![The last 10% search results requires 90% of the cost to cover](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/90-10-rule-perception-vs-reality-19.png#center)


#### Why build a search engine now?

##### Cost 

VPS service with reasonable compute power is much better compare to the last decade. [unisearch.cc] demonstrate you can run a sort of working service in 2 core VPS under 30 USD per month.

##### Internet maturity

When these search engine first comes out the web is still simple (mostly text) with a very open garden. For so crawler like googlebots bascially roams the entire internet freely. However, building a new bots are much challenging and more platform are blocking bots.

##### How do you define good

With the rise of GPT-3 models, linear algebra writes text that are more richer than human does, existing ranking method that focus in content may not be suitable anymore. What we should rank instead should be relevancy over years, content which was relevant after years and years would rank higher. Since the usable internet has exist for over 30 decades, I believe there's enough info to cover all the needed query. The missing key is only a good filter to sift out the noise.


#####  SEO, keyword spam, online spam is much different that what's 90s. 

Gaming google rank is becoming much more complex than before, these are some new methods to game. 

* Content translation : csdn.net translate github issues and show it as a website

* Medium, pixnet.net, reddit.com has so many trash content that the good ones are hardly searchable or being ignored

* Trend and traffic attract shit content and makes the whole internet sucks

### Solutions?

Well, all roads lead to Rome, you can surely make a text search engine today using swarms of elastic search for 5000 a month or [host it on S3 for under 1000 USD](https://quickwit.io/blog/commoncrawl/). Side story: this link took me 10+ queries on google.

But this only handle the retrieval part, but you still need to rank it base on other info ( quality, spam-ness, relevancy ). This is where additional components such as page rank system comes in. On the other hand, you will need to handle semantic retrieval where it retrieve results of the same semantic meaning of the query but no overlapped words/characters. If none of your search engine can do these function : huge coverage, semantic search, info box, you will be criticize as a bad search engine.

Adding components to every steps will increase the cost of maintainence and results in higher wall garden out of the reach of indie dev. I am currently testing out is neural network search (wait before you read my argument). 

Why neural networks is good:

* high capcity than I anticipate

    - My experiments shows a few million weights of text encoder would be enough to encode semantics and exact word search

* Improvement in vector search

    - new algorithm such as FAISS, annoy makes vector distance search complexity low enough I can run it on a 2 core VPS

* Simplicity

    - I only need to maintain one index table ( the vector table) which maps to websites, images, academic paper, video, audio.

And there's of course we have some issues:

* Hard to hand tune or update

    - Update or model revision upgrade requires re-running the entire vector table

    - Probably I need some trick or heuristic method to formulate the query such that it won't tricked by some random weird text (adverserial attack examples)

* Its probably not GDPR or Europe compliant

    - No idea what does my model learns

* Training complexity, since adding one modularity or search will requires adding new losses. It will become a multi task learning problem hindering the performance for each task.

## Is this a good solution?

No, probably this is bad idea, I would continue to experiments with this more later. 

Built a better search engine for the truth not propaganda.


### List of other materials I found about designing a search engine

* [Cliqz blog](https://0x65.dev/) - detail writeup about how they tackle different challenges in modern search engine

* [Vespa](https://vespa.ai/) - Yahoo open sourced their search engine