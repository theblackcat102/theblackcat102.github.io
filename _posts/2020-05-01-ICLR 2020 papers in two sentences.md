---
keywords:
  - ICLR 2020
  - research
  - paper
  - summary
comments: true
title: ICLR 2020 papers in two sentences
---

This is a list of papers I went through during International Conference on Learning Representations (ICLR) 2020. I want to thank ICLR organizer for selecting me as a volunteer.


####  Your classifier is secretly an energy based model and you should treat it like one*

This paper propose to learn probability estimation as a joint probability function $$p(x,y), p(x)$$ (JEM)  as  energy function instead of joint probability $$p(x \| y)$$, results show such method improve out of distribution detection, robust against adversarial attack and improved model calibration ( if the predictive confidence match with mis-classification rate ). Input x sampling is approximated via Stochastic Gradient Langevin Dynamics, JEM require careful tuning of hyper parameters as well as regularization for stability. 

*according to the website manager this ICLR virtual poster receives more than 1k visits traffic ( average poster visit is 400 )




####  Towards Hierarchical Importance Attribution: Explaining Compositional Semantics for Neural Sequence Models

explanation via weighted value is not enough and introduce a hierarchical explanation model in NLP. The explanation is done via sampling  


[github code](https://github.com/INK-USC/hierarchical-explanation)


[open review](https://openreview.net/pdf?id=BkxRRkSKwr)


#### ELECTRA: Pre-training Text Encoders as Discriminators Rather Than Generators

Train LM to discriminate switched words from input text. Experiments shows ELECTRA converge faster than masked language model BERT.




####  LAMOL: LAnguage MOdeling for Lifelong Language Learning

Solve catastrophic forgetting by self training language model to generate previous tasks output answer as a way to force model to retain representation of the previous tasks. Results shows LAMOL can reach lifelong learning upper boundary performance ( multi task learning )




####  Thieves on Sesame Street! Model Extraction of BERT-based APIs

Basically replicate any NLP service using BERT as base, you can replicate their model by minimal costs simply calling their API. Ways to counter this is 1. Watermark, output wrong answer for 0.1% of inputs, 2. Membership classification, output random output for non member inputs 




####  ALBERT: A Lite BERT for Self-supervised Learning of Language Representations

Instead of stack layers of self attention module represent them as a recurrent form. Other strategy such as matrix factorized embedding are introduced to reduce more hyperparameters.




####  Mixout: Effective Regularization to Finetune Large-scale Pretrained Language Models

mix dropout networks output with the original networks output by a probablity p. In a sense it weakens some connection by a probability for regularization.




####  You CAN Teach an Old Dog New Tricks! On Training Knowledge Graph Embeddings

Study work in KG embeddings and affects of their training techniques and provide a framework to benchmark all previous KG embeddings in a same environment. Results found 2011 model RESCAL can reach state of the art by applying better training method.


[github code ](https://github.com/uma-pi1/kge)


[open review](https://openreview.net/pdf?id=BkxSmlBFvr)




####  Massively Multilingual Sparse Word Representations

Introduce a multilingual word vector alignment learned through matrix factorization ( semantic atom x sparse word representation ). Alignment is archive through anchoring the semantic atoms of all other languages with a common source language. 




####  Multilingual Alignment of Contextual Word Representations

Learn multilingual alignment via parallel corpus and create language pairs between source and target word and minimize the distance between pairs as well as the target word and the original model vector to prevent degenerate results.  



####  Inductive Representation Learning On Temporal Graph

Proposed to learn graph represention through time via a reversible time representation function ( kernel ), such method allows inductively infer any node feature at any given time. Based on previous GraphSAGE work, the proposed model can infer any unseen node through inductive method ( Attention in both neighbour and time dimension ) 



#### Pretrained Encyclopedia: Weakly Supervised Knowledge-Pretrained Language Model

A simple entity augmentation method to capture knowledge relations ( entity 1 -> relation -> entity 2 ) by replacing entity in a article with another to force language model to learn real world "knowledge". 


