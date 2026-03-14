---
title: "Expected Harm: Rethinking Safety Evaluation of (Mis) Aligned LLMs"
collection: publications
permalink: /publication/2026-02-01-expected-harm
excerpt: 'We introduce Expected Harm metric that combines threat severity with execution likelihood, revealing that models exhibit Inverse Risk Calibration—disproportionately refusing difficult-to-execute threats while remaining vulnerable to easily-executable ones. This miscalibration increases jailbreak success rates by up to 2×.'
date: 2026-02-01
category: conferences
venue: 'arXiv preprint'
paperurl: 'https://arxiv.org/abs/2602.01600'
citation: 'Chen, Y.S., Tam, Z.R., Wu, C.K., &amp; Chen, Y.N. (2026). &quot;Expected Harm: Rethinking Safety Evaluation of (Mis) Aligned LLMs.&quot; arXiv preprint arXiv:2602.01600.'
---

<a href='https://arxiv.org/abs/2602.01600'>Download paper here</a>

We challenge conventional LLM safety evaluation that relies solely on threat severity. We introduce Expected Harm, a metric combining severity assessment with execution likelihood—the conditional probability of a threat being realized. Through empirical analysis, we identify Inverse Risk Calibration, revealing that models exhibit disproportionately strong refusal behaviors for difficult-to-execute threats while remaining vulnerable to easily-executable ones. By exploiting this miscalibration, we increased existing jailbreak attack success rates by up to 2×. Using linear probing, we discovered that models encode threat severity in their internal representations but lack any distinguishable encoding of execution cost, making them fundamentally unable to distinguish between high and low-likelihood threats.

Recommended citation: Chen, Y.S., Tam, Z.R., Wu, C.K., & Chen, Y.N. (2026). "Expected Harm: Rethinking Safety Evaluation of (Mis) Aligned LLMs." arXiv preprint arXiv:2602.01600.
