---
permalink: /
title: "Zhi Rui Tam"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

Research Scientist @ Appier AI Research. 


I explore Large Language Models (LLMs) with a unique perspective shaped by my multilingual background (native in Chinese, proficient in English, Cantonese, and Malay). My research focuses on understanding and advancing LLMs across multiple dimensions:

- LLM Foundations & Behavior – I investigate the fundamental aspects of LLMs, including their behavioral patterns ([Let me speak freely](https://arxiv.org/abs/2408.02442), [I need help](https://arxiv.org/abs/2407.14767)), post-training optimization, and emergent capabilities as language agents. My work spans both academic research and industrial applications, contributing to our understanding of how these models develop and deploy their linguistic capabilities.

- Multilingual Understanding – Drawing from my multilingual background, I explore how LLMs acquire and process cross-linguistic knowledge ([TMMLU+](https://openreview.net/forum?id=95TayIeqJ4#discussion), [OpenAssistant](https://proceedings.neurips.cc/paper_files/paper/2023/file/949f0f8f32267d297c2d4e3ee10a2e7e-Paper-Datasets_and_Benchmarks.pdf)). This research not only advances our technical understanding of language models but also provides insights into human language acquisition and processing.

- Applied AI Experience – Prior to my focus on LLMs, I've worked across diverse areas of AI, including keyword generation, search optimization, AutoML, and Generative Adversarial Networks (GANs), bringing a broad perspective to my current research.

I advocate for viewing LLMs as sophisticated learning systems that transcend simple n-gram pattern recognition, capable of genuine generalization beyond their training data. My research aims to bridge the gap between theoretical understanding and practical applications in multilingual AI systems.


Multilingual
======

[Openassistant conversations-democratizing large language model alignment](https://proceedings.neurips.cc/paper_files/paper/2023/file/949f0f8f32267d297c2d4e3ee10a2e7e-Paper-Datasets_and_Benchmarks.pdf)

We are the first group to create a full RLHF pipeline to train multilingual instruct following LLMs which contain fully permissive license for supervised finetune dataset, human preference labeling. This dataset consist of 161,443 messages in 35 different languages, annotated with 461,292 quality ratings, resulting in over 10,000 complete and fully annotated conversation trees. The corpus is a product of a worldwide crowd-sourcing effort involving over 13,500 volunteers. Accepted by Neurips D&B 2023 (Oral)


[TMMLU+: An Improved Traditional Chinese Evaluation Suite for Foundation Models](https://openreview.net/pdf?id=95TayIeqJ4)

TMMLU+, a new benchmark designed for Traditional Chinese language understanding. TMMLU+ is a multi-choice question-answering dataset with 66 subjects from elementary to professional level. Accepted by COLM 2024


Large Language Models
======
[Let me speak freely? a study on the impact of format restrictions on performance of large language models](https://arxiv.org/abs/2408.02442)

We found that stricter format constraints generally lead to greater performance degradation in reasoning tasks accross different language models trained by different institute. Specifically, we evaluate LLMs’ performance when restricted to adhere to structured formats versus generating free-form responses across various common tasks (classification, reasoning). Accepted by EMNLP 2024 Industry Track


[StreamBench: Towards Benchmarking Continuous Improvement of Language Agents](https://arxiv.org/abs/2406.08747)

We introduce StreamBench, a pioneering benchmark designed to evaluate the continuous improvement of LLM agents over an input-feedback sequence. StreamBench simulates an online learning environment where LLMs receive a continuous flow of feedback stream and iteratively enhance their performance. Accepted by Neurips D&B 2024

[I Need Help! Evaluating LLM's Ability to Ask for Users' Support: A Case Study on Text-to-SQL Generation](https://arxiv.org/abs/2407.14767)

We explore whether LLM can proactively ask for user help, namely decide whether the current context is not enough to fullil user requirements (such as missing values). We propose metrics to evaluate the trade-off between performance improvements and user burden, and investigate whether LLMs can determine when to request help under varying information availability. Our experiments show that without external feedback, many LLMs struggle to recognize their need for user support. Accepted by EMNLP 2024

Generative Adversarial Network
======

[Gradient Normalization for Generative Adversarial Networks](https://openaccess.thecvf.com/content/ICCV2021/papers/Wu_Gradient_Normalization_for_Generative_Adversarial_Networks_ICCV_2021_paper.pdf)

Gradient normalization is a normalization term used to stabilize the instability training of GANs by imposing a hard 1-Lipschitz constraint on the discriminator function, which increases the capacity of the discriminator. Accepted by ICCV 2021

[Character-preserving coherent story visualization](https://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123620018.pdf)

We propose a new framework named Character-Preserving Coherent Story Visualization (CP-CSV) to generate frames of story image which preserve the global consistency of the characters and scenes. CP-CSV effectively learns to visualize the story by three critical modules: story and context encoder (story and sentence representation learning), figure-ground segmentation (auxiliary task to provide information for preserving character and story consistency), and figure-ground aware generation (image sequence generation by incorporating figure-ground information). Moreover, we propose a metric named Fr´echet Story Distance (FSD) to evaluate the performance of story visualization. Accepted by ECCV 2020

