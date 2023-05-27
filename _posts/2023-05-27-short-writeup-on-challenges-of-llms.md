---
keywords:
    - large language model
    - llama
    - open source
    - thoughts
comments: true
title: Short writeup of recent challenges found in LLMs models (May 2023)
---

TLDR bullet points by GPT-4, so you don't need to wait for the plugins to generate it for you.

1. Large Language Models (LLMs) like GPT-4 still face issues in search results relevance, tool usage, and planning, limiting their effectiveness for real work situations.
2. OpenAI could use more targeted training and data generation to improve LLM performance in these areas, while the open-source community needs clever solutions to keep up with limited budgets.
3. Although current limitations persist, collaborative efforts within the open research community could potentially address these issues and help accelerate AI development.

You could read it and judge whether its useful or not

Recently I have been spending more time reading than training LLMs (Large Language Models) as research publication in these domain started to surface due to hype started since release of ChatGPT around Nov 2022. 

However, from myself and my peers personal encounters with employing AutoGPT to handle **real world** problems, the results more often than not dissapoints me. Of course don't take me on face value that GPT-4 is bad, its still useful for other stuff but certainly not the job cutting excuse C-level came up to fire normies ~~ and not that company is burning out of cash~~.

<p align="center">
<img src="https://github.com/theblackcat102/theblackcat102.github.io/blob/master/images/1685149395989.png?raw=true" height=400 stylesheet="center">
</p>

### Reference to retrieved materials

[Luo, Hongyin et al. “SAIL: Search-Augmented Instruction Learning.”](https://arxiv.org/abs/2305.15225) recently shows search results based response have problem with selecting the relevant reference out from the search result. This study shows that event ChatGPT with search sometimes failed to reference the relevant answer and started to hallucinate. Even in Bard with retrieval, the result also contain some imaginary facts [tweet](https://twitter.com/adrianhon/status/1638214826957611014). 

### Tool use is still a problem

Since the release of [Schick, Timo et al. “Toolformer: Language Models Can Teach Themselves to Use Tools.”](https://arxiv.org/abs/2302.04761), there are many research and commercial attempt in "teaching" LLMs to use as many online tools as possible. For example, knowing when to use search engine is pretty useful to solve the [knowledge cutoff problem](https://news.ycombinator.com/item?id=35216648).

Recent release of chatgpt plugin found that LLM more often than not fails to execute the plugin correctly [reddit post](https://www.reddit.com/r/ChatGPT/comments/13jgd8t/new_web_browsing_failures/). I once saw a tweet about the success rate for plugins but failed to find it again, so you have to take me at face value for this single reddit post. Ideally, we should have a consensus of how plugin are tested and better a review function like play store and app store have been doing for years. But the underlying problem might be these LLMs are not trained to handle complex naming scheme or outlier inputs which took the attention way from the models and started to output gibberish results.

In the open source domain, there are datasets or ideas in teaching models to use tools and more specifically increase the success rate of tool use ( generate a correct requests, successfully output the reply based on the response from the requests )

* [Patil, Shishir G. et al. “Gorilla: Large Language Model Connected with Massive APIs.”](https://arxiv.org/abs/2305.15334)

* [Symbolic finetuning from google brain might help](https://twitter.com/richardsocher/status/1658946465233002496?s=21)


### Need more dataset in planning

When AutoGPT first came up on twitter, most SV or WSJ investors got pumped up as it promised the future where companies could fire all their expensive eng and remove the perks such as massage, business class flight expenditure from their quarterly reports.

But the experience for me and my peers are complaining about GPT-4 kept getting [stucked in a loop](https://github.com/Significant-Gravitas/Auto-GPT/discussions/1292) where the "agent" kept repeating itself on the same sub task. Disclaimer, most of us tested on real programming challenge we faced IRL and not the generic planing a trip to somewhere or write a MVP app/plugin. 

Recent paper by [Valmeekam, Karthik et al. “Large Language Models Still Can't Plan (A Benchmark for LLMs on Planning and Reasoning about Change).”](https://arxiv.org/pdf/2206.10498.pdf) found that neither of the LLMs are able to came up with a plan to solve a simple toy problem. This is the evidence study which AutoGPT is too early for its prime time and represent a overhype signal for this.

For OpenAI they could pay their sub contractors to generate more plaining questions and ~~overfits~~ teach the model to do plaining. But for open source community, its hard to came up with such expensive labeling solution so we might need a more clever way to generate such dataset.

## Final notes

The 3 issues I mentioned above aren't unsolvable problem, heck the open source community could waited for the next GPT update and [simply clone them](https://arxiv.org/abs/2305.15717). But I think it would showcase the speed in where open research could cowork together and solve the solution through clever tricks and prompting which solving the problem within a small budget as compare to the closed AI research teams.

<p align="center">
<img src="https://github.com/theblackcat102/theblackcat102.github.io/blob/master/images/apes-together-strong-0p1sf.gif?raw=true" height=300 stylesheet="center">
</p>


* definition of **real work** is not writing test cases nor template code for CRUD app. some examples of real work: write a viable solution for finding the best voted rank of orders, parse simple text responses, etc

