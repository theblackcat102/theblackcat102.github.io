---
keywords:
  - common crawl
  - crawler
  - reproduce
  - interesting
  - CCNet
  - corpus
  - nlp
  - raw text
  - data mining
  - multilingual
comments: true
title: Extract high quality corpus from common crawl efficiently using CCNet
cover_image: https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/jonathan-SwVkmowt7qA-unsplash.jpg
---

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/jonathan-SwVkmowt7qA-unsplash.jpg)


Pretraining language model has been proven a efficient way to improve any NLP tasks shown in MultiFit, XLNet, BERT, GPT-1, GPT-2. These models are usually pretrained on Wikipedia Corpus as it's high quality and openly available but most importantly it's diverse enough in terms of semantic and syntax use. Amazon Review dataset are also quite good however, it's limited only in English while Wikipedia corpus is available in many other less common language such as Malay. 

However, there's a rise of using [Common Crawl project](https://commoncrawl.org/) raw text as an alternative to Wikipedia corpus. Recently T5 (Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer
) declared as SOTA(state of the art) model in [MultiNLI](https://paperswithcode.com/sota/natural-language-inference-on-multinli) (natural language inference) and CNNDM (document summarization) surpassing XLNet, ALBERT, RoBERTa score. 

One of the pretrained datasets T5 used is C4 which is text derived from Common Crawl. C4 is proven to obtain better score than pretraining on Wikipedia text. However, this dataset is only available in English while Common Crawl contain many other lanaguages. Thanks to Facebook recent paper CCNet we are able to get a clean corpus in many other language. 

## CCNet : Extracting High Quality Monolingual Datasets from Web Crawl Data


![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/CCNet_pipeline.png)

CCNet extract a clean text from Common Crawl wet files (raw text of a website) and clean them using a pretrained 5-gram model pretrained on Wikipedia over 18 different languages by filtering perplexity lower than an given threshold. fastText is used for language identification and deduplication using hash of the content. Overall, this is a pretty simple idea but hard to execute it perfectly, I recommend anyone interested in reproducing CCNet read through their code first, you can always learn a few or two from this. 

As we mortal individuals trying to replicate this work is hard as the author of CCNet uses a total of 16000 processors to finish indexing and extracting. Download and storing wet files requires 7TB of storage while processing requires more than 64G of memory. With the last of my free google cloud credit, I set up to make this work within limited resource using a 8 core VM instance and another 4 core instance for small language corpus. The reason I split them and not using a more powerful instance is due to the quota limit on free credits. But hey, it's the speed is still much better than my delay in Taiwan.


For anyone who tried to replicate CCNet these are some of my thoughts and tricks:

1. Memory leak of some kind / Memory error

  If you are using high process count, each process will consume an estimate of 32G at max ( limit impose in unminify ). Hence, create a large swap is crucial. In extracting English corpus, running a 16 process will consume about 240G of swap space with full memory use.

2. Common Crawl Snapshot download

  snapshot size for Common Crawl 2019-09 ( the snapshot which we can reproduce without reindexing them ), is roughly 7.2TB. If your compute unit is too far from AWS S3 server where this snapshot is stored, you will spent a few days in downloading them. 

3. Only one language at a time

  If you have limited memory or limited cpu( < 100), you should always crawl one language at a time.

4. Monitor your cpu usage

  When the extraction is nearly finished, cpu usage will drop as the density of article became very sparse and process spend most of the time going through bits of text accross different WET file. I will advice you to stop the extraction and continue your next language.


## Results

My final common crawl wet file size is 7TB, roughly matched the snapshot from 2019 February. Meaning the extraction process did went through most of the wet files despite only extracting a fraction of the language corpus available in Common Crawl.

I only selectively choose these selective language as crawling all the available language will break my ~~bank~~ google free credits. The total hours of crawling is estimated one week, including thinkering with different configuration and setups.

WET files of a snapshot are sharded as a size of 120MB file, all languages are separated in each different files. Hence certain language will took longer time to finish extraction because we have to look through lots of different wet files only for a few paragraph of text. Hence, I will stop any extraction process if all cpus usage are no longer 100% to ensure highest efficiency (time and bandwidth is money, tick tock tick..).

The breakdown of all each language compressed size are shown as follow:

| en  | ru  | zh  | de | fr  | ja  | es  | th  | it  | pt  | ko | id | ar | fi | ms |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 148G  |  28G |  27G | 13G  | 9.4G  | 8.1G  | 7.5G  | 3.5G  |  2.7G  | 2.2G  |  1.8G | 0.26G | 0.25G  | 65M | 18M |

Total corpus size is 334.71 GB of compressed corpus, not a lot compared to CCNet paper results, but way more than Wikipedia's offers.

## Price breakdown

All my instance and cloud storage bucket are located in Iowa(US) for lowest cost possible. N2 cpu is chosen for faster clock speed (2.8GHz vs 2Ghz ) than N1. Although CCNet paper written 3.7TB of corpus is extracted, since I am not extracting all the language nor the full corpus (explained previously), I can get away with a smaller disk space 1TB instead of 4TB.

| Core  | Memory  | Disk Space  | Location  | Cost per hour |
|---|---|---|---|---|
| 8 | 64G  | 1T | Iowa  |  0.88 |
| 4  | 32G  | 50G  |  Iowa | 0.27  |

Here's my cost breakdown of computing cost. About 20 dollars per day. 

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/cost_breakdown.png)


And here's my cost of using 7TB of cloud storage space. Because local transfer between cloud storage and compute instance is free, my average daily cost lies around 5 dollars with the exception I tried to download common crawl from my workstation as well in November 18. Remote access cost more than I imagined before I stop it, it already cost me 71 dollars.

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/cloud_storage_cost.png)

Overall, my total expenditure is roughly 178 dollars (minus the extrac) .If isn't because of my mistake I would be able to extract more text corpus. But since it's free (thanks Google) and partly due to my own mistake, I will get a free pass this time.

