---
keywords:
  - machine learning
  - neural networks
comments: true
title: List of machine learning slides by myself
---

This is a collections of slides I made during the past few years for group study or paper presentation sessions. 


# Paper Presentation Slides


[Rethinking Attention with Performer](https://docs.google.com/presentation/d/1XxdLgCZiqPsvdscvV6kqh5mdK4GqDjVsE7sbOByt86Y/edit?usp=sharing)

topics : architecture

One of the aspect I doesn't like about this network is it's heavy reliant on random process theory( I have no beef with RP ) because the kernel needs to be initialize each forward pass (in theory) and the initialization include SVD calculation which makes it pretty slow on consumer workstation. Due to this reason, I haven't had any success with using this design in any of my projects. 

[Mu-Zero: Mastering Atari, Go, Chess and Shogi by Planning with a Learned Model](https://docs.google.com/presentation/d/1YqXeyZhdmtL8M3FZstN0ndIaM2UqJ0kFs4PvQsW_wUM/edit?usp=sharing)

topics : reinforcement-learning

I choosen this topic merely to introduce AlphaZero 2.0 to my peers because the idea is very clean and simple yet very powerful.

[BYOL](https://docs.google.com/presentation/d/1-AvbgmBf4kPixM6xhRCywuRvDTlzTCZzu4Wz7jlqtJ0/edit?usp=sharing)

topics : self-supervised-learning

Thanks to Yann Lecun cake image, self-supervised learning is a hot topic at that time. So I have choosen this not so intuitive learning method to present. A slight background, self-supervied learning before is mostly revolve around siamese network design. Such method has some stability issues when trained on only raw inputs ( so you need large batch size, crazy learning rate scheduling and some weird augmentations to make it work ). Before SimCLR paper, such approach is actually a good trick for small datasets since it's a good and effective regularization method to prevent overfitting. This is one the very few tricks in my sleeves for using neural network on small datasets to gain better performance than sklearn baseline.

[VQ-VAE](https://docs.google.com/presentation/d/1k_5YBC9hfWL_zBSkKn4kT6bm1KF6EkadUDKWzQoTMSY/edit?usp=sharing)

[ELECTRA: Pretraining Text Encoders as Discriminators rather than Generators](https://docs.google.com/presentation/d/1gX43j65DWJNCkRNbgTAuuMRZnU0YdwH69-pGju1YqVs/edit?usp=sharing)

topics : self-supervised-learning

[Consistency regularization for GAN](https://docs.google.com/presentation/d/1PRPg9lbTcMEaBYNSTtWM_2RSub8prZxJlD-AyuVkLvE/edit?usp=sharing)

topics : regularization, generative adversarial networks

I was participating some GANs research at that time, when I saw this paper it's so easy to implement I can't resist it. So I may as well made a presentation out of it ¯\_(ツ)_/¯


[Your classifier is secretly an energy based model and you should treat it like one ](https://docs.google.com/presentation/d/17OLmpXPU4u1_nFEW6R054qpNfq3A8zF9xVzMkbu2_QA/edit?usp=sharing)

topics : learning

This is one the very few papers I really enjoy reading in terms of flow, name and easy to run code. 


[REFORMER The efficient Transformer](https://github.com/theblackcat102/theblackcat102.github.io/raw/master/resource/presentation/REFORMER%20The%20efficient%20Transformer.pdf)

One the very few papers I presented which I ended up revisting again after a long time. When the implementation first finished by [lucidrains](github.com/lucidrains/reformer-pytorch), I tried it out on a chinese MLM learning task and have very few success. However recently I compared it again with vanilla transformer on wiki-en8 task and found reformer actually converge faster than it's origin version. This actually one the very few autoregressive transformer which actually provide significant speedup compared to recent proposal such as longformer and reformer.


# Graph Neural Networks Study Group

I was lucky enough to join a study group sharing about graph neural networks. These are some of the slides I prepared for the group study. 


[Graph classification - Part 1](https://docs.google.com/presentation/d/1FItqLQMiQgiU2rpdgJtOmNcUsJYrwSYz3E568uZBPFU/edit?usp=sharing)

[Graph classification - Part 2](https://docs.google.com/presentation/d/1k8zpnS--4ddC3vjpXuNxA_AlgCq01ndVACBbjdgr2m4/edit?usp=sharing)

[Application - Generation](https://docs.google.com/presentation/d/1icGXHEeEwrr1PbDiUf0GF38jbmNDB8tEu0nzQXwlr1Y/edit?usp=sharing)

In this slides, I will go through 4 graph generation papers with each representing a specific domain faced in generating graph. 

[Graph Pooling](https://docs.google.com/presentation/d/1aLvfSVEn0-ENcYydjp9nTjgiaK6EjlJFfDkZdhnIqDI/edit?usp=sharing)

gPool and SAGPool

[Graph Pooling - Part 2](https://docs.google.com/presentation/d/1MQJS8NrxGD5JR26T3p1TUKRIwl_32hX7Om4yCgS4aFE/edit?usp=sharing)

SortPool and EigenPool


It's 1.26 am in Taiwan, I will update the description and add more slides later 