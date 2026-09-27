---
permalink: /
title: "Zhi Rui Tam"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

PhD @ [Miu Lab](https://www.csie.ntu.edu.tw/~miulab/) under [Vivian Chen](https://www.csie.ntu.edu.tw/~yvchen/), previously Sr Research Scientist 2 @ Appier AI Research


## About Me

I'm a PhD candidate at National Taiwan University exploring Large Language Models with a unique perspective shaped by my multilingual background (native in Chinese, proficient in English, Cantonese, and Malay). I work on understanding and advancing LLMs in both academic and industrial settings.

Research-wise, I'm interested in the broad area of LLMs, with the goal of understanding model behaviors and safety while bridging the gap between theoretical understanding and practical applications. Recently, my research focuses on:

- **LLM Agents & Tool Use**: Training models that jointly create and use tools, so tool interfaces and their invocation improve together within a single policy.

- **LLM Safety & Behavior**: Investigating fundamental aspects including behavioral patterns, safety evaluation frameworks, post-training optimization, and emergent capabilities as language agents.

- **Multilingual Understanding**: Exploring how LLMs acquire and process cross-linguistic knowledge, advancing both technical understanding and insights into human language processing.

<!-- Previously I have worked on keyword generation, search optimization, AutoML, and Generative Adversarial Networks. I advocate for viewing LLMs as sophisticated learning systems that transcend simple n-gram pattern recognition, capable of genuine generalization beyond their training data. -->

## News

- **[Sept. 2026]** 1 [paper](https://tool-use-smith.github.io/) accepted by NeurIPS Main, 2 accepted by NeurIPS ED Track ([paper](https://expectedharm.github.io/) Spotlight)
- **[May. 2026]** One findings [paper](https://aclanthology.org/2026.findings-acl.1830/) accepted by ACL 2026.
- **[Mar. 2026]** One [paper](https://aclanthology.org/2026.iwsds-1.7.pdf) accepted by IWSDS 2026. (best paper)
- **[Feb. 2026]** One [paper](https://ieeexplore.ieee.org/abstract/document/11463343/) accepted by ICASSP 2026.
- **[Sep. 2025]** One [paper](https://arxiv.org/abs/2501.14315) accepted by NeurIPS 2025.
- **[Jun. 2025]** One findings [paper](https://aclanthology.org/2025.findings-acl.1031/) accepted by ACL 2025.
- **[Nov. 2024]** Two papers ([1](https://aclanthology.org/2024.emnlp-industry.91), [2](https://arxiv.org/abs/2407.14767)) accepted by EMNLP 2024.
- **[Sep. 2024]** One [paper](https://openreview.net/forum?id=8hUUy3hoS8) accepted by NeurIPS D&B 2024.
- **[Jun. 2024]** One [paper](https://arxiv.org/abs/2403.01858) accepted by COLM 2024.
- **[Oct. 2023]** One [paper](https://proceedings.neurips.cc/paper_files/paper/2023/hash/949f0f8f32267d297c2d4e3ee10a2e7e-Abstract-Datasets_and_Benchmarks.html) accepted by NeurIPS D&B 2023 (Oral).


## Selected Research

**[Joint Optimization of Tool Creation and Use for Large Language Model Agents](https://tool-use-smith.github.io/)**
**ZR Tam**, CY Lin, YN Chen, SH Hua, HY Lee
*NeurIPS 2025 Main*
#Agents #ToolUse #RL

We propose SMITH, a reinforcement learning framework that jointly trains tool creation and tool use within a single policy, with separate reward axes for schema, code, and outcome failures. A 4B model trained on 13 procedural reasoning tasks reaches 79.9 macro-average accuracy on held-out tasks—outperforming an untrained 30B tool-writer—and its tools transfer to models as small as 350M.


**[Expected Harm: Rethinking Safety Evaluation of (Mis)Aligned LLMs](https://expectedharm.github.io/)**
YS Chen\*, **ZR Tam**\*, CK Wu, YN Chen
*NeurIPS 2026 ED (Spotlight)*
#Safety #Evaluation #Alignment

We introduce Expected Harm metric combining severity with execution likelihood, revealing Inverse Risk Calibration where models refuse difficult-to-execute threats while remaining vulnerable to easily-executable ones. By exploiting this miscalibration, we increased jailbreak success rates by up to 2×.

**[Let me speak freely? A study on the impact of format restrictions on performance of large language models](https://arxiv.org/abs/2408.02442)**
**ZR Tam**\*, CK Wu\*, YL Tsai, CY Lin, HY Lee, YN Chen
*EMNLP 2024 Industry Track*
#Behavior #Constraints

We found stricter format constraints generally lead to greater performance degradation in reasoning tasks across different language models, evaluating performance when restricted to structured formats versus free-form responses.

**[TMMLU+: An Improved Traditional Chinese Evaluation Suite for Foundation Models](https://openreview.net/pdf?id=95TayIeqJ4)**
**ZR Tam**, YS Chen, CK Wu, TH Yeh, WC Cheng, BY Lin, CH Li, MC Yeh, YN Chen
*COLM 2024*
#Multilingual #Benchmark

A new benchmark designed for Traditional Chinese language understanding with 66 subjects from elementary to professional level, improving evaluation of foundation models on Traditional Chinese.

**[OpenAssistant Conversations - Democratizing Large Language Model Alignment](https://proceedings.neurips.cc/paper_files/paper/2023/file/949f0f8f32267d297c2d4e3ee10a2e7e-Paper-Datasets_and_Benchmarks.pdf)**
Andreas Köpf, ..., **ZR Tam**, ... et al.
*NeurIPS D&B 2023 (Oral)*
#Multilingual #RLHF #Dataset

First full RLHF pipeline to train multilingual instruct-following LLMs with 161,443 messages in 35 languages, annotated with 461,292 quality ratings from 13,500 volunteers worldwide.


## Research Interests

LLM Agents & Tool Use · LLM Safety · Behavioral Analysis · Audio Language Models · Multilingual NLP · Model Evaluation · Human-AI Interaction · Bias & Fairness


## Misc

I'm also involved in [GlobalPIQA](https://arxiv.org/abs/2510.24081) project (2026 NeurIPS ED) contributing Malay dataset.


