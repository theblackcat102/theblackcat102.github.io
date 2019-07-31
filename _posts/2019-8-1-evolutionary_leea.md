---
keywords:
  - NLP
  - n-grams
  - language model
  - brown clustering
comments: true
title: Note Simple Evolutionary Optimization Can Rival Stochastic Gradient Descent in Neural Networks (LEEA)
---

This paper introduce some insight about why a gradient optimization algo such as SGD works so well and how evolution algo (EA) can perform as well as gradient based algo.
 
 
EA learning method is as follows: 
 
 1. A population of individual of the models are generated and a fitness score is evaluated on all individuals. 
 
 2. Only top N individuals are selected and sexual reproduction and asexual reproduction is used to generate a new generation 
 
 3. repeat step 1,2 until convergence is reached.
 
SGD has always touted that it will find local optimal solution, however, in a ANN model, there’s lots of weight configuration that finding a local optimal solution should not result in state of the art result as seen today. The argument given is that there’s many optimal path to escape from optimal solution such that the final result isn’t a local optima. They however suggest that that SGD the real culprit should be saddle point problem which other gradient based algo such as RMSProp, Adagrad etc aimed to solve. 

Since EA is inherently immune to saddle point problem because no gradient are calculated in the training process. 

LEEA proposed that if SGD can optimize model using partial dataset, EA should also able to generate a new generation using partial dataset. Making EA computationally same as SGD.

However, mini batch evaluation method in LEEA may result in certain individual to lost fit. Hence the fitness evaluation is calculated based on current mini batch and their ancestors score on their mini batch called fitness inheritance. This method include information from their ancestor mini batch which prevent bias on the current mini batch.

                $$f^{'} = \frac{ f_{p1}+f_{p1} }{2}(1-d)+f$$

$$f^{'}$$ is the modified fitness score where $$f$$ is the fitness score, with $$f_{p1}, f_{p2}$$ as the individual parent 1 and 2 fitness score. $$d$$ is a decay hyper parameter.
