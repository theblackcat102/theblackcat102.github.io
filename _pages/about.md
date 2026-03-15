---
permalink: /
title: "Zhi Rui Tam"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

PhD @ [Miu Lab](https://www.csie.ntu.edu.tw/~miulab/) under [Vivian Chen](https://www.csie.ntu.edu.tw/~yvchen/), concurrently Sr Research Scientist @ Appier AI Research


## About Me

I'm a PhD candidate at National Taiwan University exploring Large Language Models with a unique perspective shaped by my multilingual background (native in Chinese, proficient in English, Cantonese, and Malay). I work on understanding and advancing LLMs across multiple dimensions at both academic and industrial settings.

Research-wise, I'm interested in the broad area of LLMs and speech AI, with the goal of understanding model behaviors and safety while bridging the gap between theoretical understanding and practical applications. Recently, my research focuses on three aspects:

- **Audio Language Models**: Understanding unique challenges and biases in audio-based LLMs, examining how paralinguistic cues affect model behavior and investigating architectural limitations in multi-turn dialogue systems.

- **LLM Safety & Behavior**: Investigating fundamental aspects including behavioral patterns, safety evaluation frameworks, post-training optimization, and emergent capabilities as language agents.

- **Multilingual Understanding**: Exploring how LLMs acquire and process cross-linguistic knowledge, advancing both technical understanding and insights into human language processing.

<!-- Previously I have worked on keyword generation, search optimization, AutoML, and Generative Adversarial Networks. I advocate for viewing LLMs as sophisticated learning systems that transcend simple n-gram pattern recognition, capable of genuine generalization beyond their training data. -->

## News

- **[Mar. 2026]** One paper accepted by IWSDS 2026.
- **[Feb. 2026]** One paper accepted by ICASSP 2026.
- **[Sep. 2025]** One paper accepted by NeurIPS 2025.
- **[Jun. 2025]** One finding paper accepted by ACL 2025.
- **[Nov. 2024]** Two papers accepted by EMNLP 2024.
- **[Sep. 2024]** One paper accepted by NeurIPS D&B 2024.
- **[Jun. 2024]** One paper accepted by COLM 2024.
- **[Oct. 2023]** One paper accepted by NeurIPS D&B 2023 (Oral).


## Selected Research

**[Expected Harm: Rethinking Safety Evaluation of (Mis)Aligned LLMs](https://arxiv.org/abs/2602.01600)**
YS Chen, **ZR Tam**, CK Wu, YN Chen
*arXiv preprint, Feb 2026*
#Safety #Evaluation #Alignment

We introduce Expected Harm metric combining severity with execution likelihood, revealing Inverse Risk Calibration where models refuse difficult-to-execute threats while remaining vulnerable to easily-executable ones. By exploiting this miscalibration, we increased jailbreak success rates by up to 2×.

**[The Context Trap: Why End-to-End Audio Language Models Fail Multi-turn Dialogues](https://aclanthology.org/2026.iwsds-1.7/)**
**ZR Tam**, WY Chang, YN Chen
*IWSDS 2026*
#Audio #Dialogue #Architecture

We systematically compare E2E audio LMs with modular systems, revealing that E2E configurations consistently underperform due to context maintenance and topic tracking deficiencies, challenging assumptions about their superiority over modular approaches.

**[MedVoiceBias: A Controlled Study of Audio LLM Behavior in Clinical Decision-Making](https://arxiv.org/abs/2511.06592)**
**ZR Tam**, YN Chen
*ICASSP 2026*
#Audio #Bias #Healthcare

Testing 170 clinical cases across 36 voice profiles, we found surgical recommendations varied by up to 35% between audio and text inputs, with age-related disparities reaching 12%, raising serious concerns about perpetuating healthcare disparities.

**[Let me speak freely? A study on the impact of format restrictions on performance of large language models](https://arxiv.org/abs/2408.02442)**
CK Wu, **ZR Tam**, HC Huang, YN Chen
*EMNLP 2024 Industry Track*
#Behavior #Constraints

We found stricter format constraints generally lead to greater performance degradation in reasoning tasks across different language models, evaluating performance when restricted to structured formats versus free-form responses.

**[I Need Help! Evaluating LLM's Ability to Ask for Users' Support](https://arxiv.org/abs/2407.14767)**
**ZR Tam**, CK Wu, YS Chen, TH Yeh, HY Lee, YN Chen
*EMNLP 2024*
#Behavior #HCI

We explore whether LLMs can proactively ask for user help and propose metrics to evaluate the trade-off between performance improvements and user burden. Our experiments show that without external feedback, many LLMs struggle to recognize their need for support.

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

Audio Language Models · LLM Safety · Behavioral Analysis · Multilingual NLP · Model Evaluation · Human-AI Interaction · Bias & Fairness


## Misc

I'm also involved in [GlobalPIQA](https://arxiv.org/abs/2510.24081) project contributing Malay dataset.

