---
keywords:
  - NLP
  - language model
  - language Understanding
  - multi-task learning
  - multi-task neural network
  - mt-dnn
comments: true
title: Summarizing MT-DNN the state of the art model in language tasks before XLNet.
---


Multi-Task deep neural network (MT-DNN) for deep language understanding proposed by Microsoft achieve SOTA results in April on 10 language tasks ( GLUE, SNLI, … ). The author purpose that multi task learning which used in computer vision domain before to achieve state of the art result, can also be used to improve language understanding scores.

paper : [https://arxiv.org/pdf/1901.11504.pdf](https://arxiv.org/pdf/1901.11504.pdf)

code : [https://github.com/namisan/mt-dnn](https://arxiv.org/pdf/1901.11504.pdf)

*Core Idea: Pretraining → Multi task learning (classification, semantic similarity, pairwise) → fine tune (GLUE, SNLI). Multi tasks learning will act as a regularizer mechanism.*
 
#### Stage 1 Pretraining 

The pretraining stage is same as BERT paper which is token masking and next sentence prediction. In this stage the weights for multi task learning is not added. 

#### Stage 2 Multi Task Learning

In this stage, additional weight for each tasks are added to the output of BERT model. A total of 4 tasks are used in this stage, these tasks include sentence classification, semantic similarity, relevance ranking output, pairwise text classification. The data source for these tasks came from 9  different datasets. 

All datasets are mixed together, we only sample mini batch from one of the tasks, the loss for the tasks are calculated and gradient are updated. 

#### Hyperparameters

Since this model is extremely huge, the purposed model was trained on 8 V100 32G of VRAM.

Encoder : BERT model, input length 512

Optimizer : adamax

Learning rate : 5e-5, learning rate decay 0.1, warm up

Max epoch : 5

Dropout : 0.1 for all tasks except MNLI 0.3, CoLa 0.05

Gradient norm clip : 1

Batch size : 32

#### Conclusion

This paper conclude that multi-task learning improve language understanding as observe in computer vision domain. However, the score presented in this paper had since be overtaken by XLNet large which do not relies on any multi-task learning. My opinion was this is likely due to the more effective design of XLNet which able to learn bidirectional relations without the pretrain-finetune discrepancy problem. The ability of able to learn long sequence from XLNet may also contribute better performance compare to the BERT model used in this paper. 
