---
title: "αTransfer: Coefficient Transfer for Efficient Model Merging"
collection: publications
permalink: /publication/2026-10-06-alpha-transfer
excerpt: 'Within the same model family, merging coefficients that work well on a small model also work well on a large one. We introduce αTransfer, which searches merging coefficients on a small proxy model and applies them directly to a larger target, giving a 6x speedup and 70% memory reduction on vision transformers and a 20x speedup and 85% memory reduction on LLMs at comparable accuracy.'
date: 2026-10-06
category: conferences
venue: 'arXiv preprint'
paperurl: 'https://arxiv.org/abs/2610.07819'
citation: 'Huang, S.C., Tam, Z.R., Lin, C.Y., Chen, Y.N., Lee, H.Y., &amp; Sun, S.H. (2026). &quot;αTransfer: Coefficient Transfer for Efficient Model Merging.&quot; arXiv preprint arXiv:2610.07819.'
---

Model merging has been a quick and efficient way to boost / hill climb model performance in several fronts (metrics). It achieve so by combining several fine-tuned checkpoints into one model by adding their task vectors (the weight difference between each fine-tuned model and the base model) back onto the base. Each task vector is scaled by a merging coefficient, and the merged model is very sensitive to those coefficients. We study how to find good coefficients for a large model without running the full search on it.

![αTransfer: search coefficients on a small proxy model, then apply them directly to the large target](/images/alpha-transfer-figures/overview.webp){: .align-center}

However finding these coefficients can be expensive if models are big or benchmarks (reward signal) are hard to eval. Evaluation-based methods like grid search or Bayesian optimization have to build and evaluate a merged model for every candidate, and each evaluation gets slower as the model grows. Gradient-based methods such as AdaMerging and DivMerge reduces the eval numbers, but the calculation of gradient require passing through all the various models. This isn't good as gradient calculation cost (memory or computation) scale linearly with model size and the total number of tasks. Since each task is its own individual model after all.

So how? Scaling law to the rescue?

The lesson from scaling laws was to run the experiments small and extrapolate the trend up by fitting lines, and so far its been quite well in predicting them (at least its used by almost all LLM labs) : [Kaplan et al.](https://arxiv.org/abs/2001.08361) and [Chinchilla](https://arxiv.org/abs/2203.15556). [μTransfer](https://arxiv.org/abs/2203.03466) found that by tuning the learning rate on a small model and, with the right parameterization we can reuses it on a large one (This is the work which inspired me to propose this idea). [DoReMi](https://arxiv.org/abs/2305.10429) picks the data mixture for an 8B model using a 280M proxy. They all rely on the same idea: some choices depend on the problem rather than on model size, so what works best on a small model is still best on a big one.

So here was my idea. Models in the same family are usually pretrained on the same corpus, so models of different sizes may learn similar internal representations of the same tasks, with the larger ones simply having more capacity. If so, fine-tuning each size on the same set of tasks should produce task vectors that relate to each other in the same way: which tasks help each other, which ones interfere, and how much each one should count. And if those relationships hold across sizes, the merging coefficients that balance them should transfer within the family too.

![Hypothesis: shared pretraining and fine-tuning tasks may preserve helpful and interfering task relationships across model sizes, allowing merging coefficients to transfer while each model keeps its own task vectors.](/images/transfer-intuition-v2.webp){: .align-center}

*The intuition behind αTransfer: if task relationships remain similar across sizes within a model family, coefficients learned on a small model may also balance the large model's own task vectors. Task relationships shown here are illustrative.*


We did a quick experiment by sweeping two task coefficients and plot the merged accuracy: SigLIP-Base and SigLIP-Large produce nearly the identical landscape. We also over sampled coefficient settings across all 8 vision tasks or 4 language tasks, the Spearman rank correlation between proxy and target accuracy is 0.79 for SigLIP-Base → SigLIP-Large, 0.84 for ViT-B/16 → ViT-L/14, and 0.90-0.94 for Qwen3-0.6B → Qwen3-1.7B/4B. A coefficient setting that ranks well on the small model usually ranks well on the large one too.

![Merged-model accuracy over a grid of two task coefficients is nearly the same for SigLIP-Base and SigLIP-Large](/images/alpha-transfer-figures/landscape-heatmap.webp)

That makes αTransfer very simple: pick a small proxy from the same family, run any existing merging method on it to find the coefficients, then apply those coefficients directly to the target model. Only the coefficients are transferred. Method-specific steps like TIES trimming or DARE masking are still applied to the target model's own task vectors. For layer-wise methods where the proxy and target have different depths, each target block takes the coefficient of the proxy block at the same relative depth, either by copying the nearest block or interpolating between neighbors.

We tested this on six merging methods (Task Arithmetic, TIES, DARE, AdaMerging, AdaMerging++ and DivMerge) across the CLIP-ViT, SigLIP and Qwen3 families. On vision models, transfer is up to 6.07x faster and uses up to 70.4% less memory, often with a negligible accuracy gap: TIES and DARE drop only 0.11 and 0.32 points on SigLIP-Base → SigLIP-Large. On Qwen3, transferring from 0.6B to 4B loses no accuracy for Task Arithmetic and TIES-Pairwise, with a 20x speedup and 85% less memory, from over 40GB down to under 6GB. Even the worst case, AdaMerging++ on ViT-B/32 → ViT-L/14 (7.02 points below direct search), is still 7.12 points above simply averaging the task vectors.

The transferred coefficients also work as a starting point when accuracy matters more than speed. In a hybrid setup, we search on the proxy first and spend a small part of the budget refining on the target. This closes all or most of the gap to direct search, while still being 1.20-1.86x faster on vision models and 2.29-4.35x faster on LLMs.

So one thing that's missing is that we didn't ended up with a satisfying explaination to why this happens from a mathematical theory standpoint. Moreover, we found that ViT-B/32 → ViT-L/14 has a weaker correlation (ρ = 0.58) and some accuracy drops, which I think input geometry and model scale would break under our initial assumptions. AdaMerging++ at extreme sparsity (keeping only 20% of parameters) also favors searching on the target directly. Another thing is that we only transferred coefficients within a single model family, while we observe the same simple single coefficient method kinda similar across various family (SigLIP and CLIP), we cannot be sure if they actually carry over across different training recipes or architectures (For example we found ResNet and ViT of CLIP doesn't transfer). 

But we are confident that our results do suggest that a good merging coefficients are mostly a property of the tasks and the model family (same data exposure on the same architecture design).

<p style="font-size: 1.25em"><a href='https://arxiv.org/abs/2610.07819'><i class="ai ai-arxiv"></i> Download paper here</a></p>

```bibtex
@article{huang2026alphatransfer,
  title={$\alpha$Transfer: Coefficient Transfer for Efficient Model Merging},
  author={Huang, Shih-Cheng and Tam, Zhi Rui and Lin, Chieh-Yen and Chen, Yun-Nung and Lee, Hung-yi and Sun, Shao-Hua},
  journal={arXiv preprint arXiv:2610.07819},
  year={2026}
}
```
