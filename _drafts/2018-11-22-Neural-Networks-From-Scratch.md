---
title: "Neural networks from scratch"
description: "Understand and implement a neural net"
layout: post
math: true
tags:
  - machine learning
  - deep learning
  - python
  - jupyter notebook
  - Mathematics
comments: true
---


Cet article va me permettre d'introduire la série d'articles et le plan, je vais aussi mettre mes notes et idées ici.

1. Binary linear classifier, montrer comment ça marche
2. Faire une transition entre le binary classifier et le concept de neurone
3. Montrer les exemples de perceptrons avec des fonctions booléennes et montrer la limite quand on veut faire des classifications non linéaires => montrer le besoin de multicouches => faire référence aux preuves
4. Introduire, formaliser les neurones :
	entrée
	poids
	additions + BIAS
	activation function

	=> change regression logistic
	=> Probability
	=> Error measurement, cross entropy
		* <https://www.reddit.com/r/MachineLearning/comments/34f23i/question_cross_entropy_vs_euclidean_distance_for/>
		* <https://en.wikipedia.org/wiki/Bhattacharyya_distance>
		* <http://www.hongliangjie.com/2012/07/12/maximum-likelihood-as-minimize-kl-divergence/>
	=> Gradient descent
	=> Back propagation
























---------------


I made [this jupyter notebook](https://github.com/GarreauArthur/ldl/blob/master/NNfromScratch.ipynb)

I was about to write an article explaining how neural nets work, and how you can
implement one from scratch using python, to demonstrate my ability to communicate
on a complex subject. But <del>idk i feel like dying today</del> there are
already tons of ressources to learn about neural net, you don't need one more.





----------------------

Building things that we don't understand.
Artificial Intelligence is more Engineering than Science.

Our knowledge of the human brain is still pretty limited.

The reason why there is AI, is because we need it.
Our own lack of understanding


Computers are limited by their power, memories and by our own inability to
understand and find programmable solutions to problems. Sometimes we know how
to find the answer, we just can't compute it. Artificial intelligence is



The first model of a neuron was made by McCullogh and Pitts in 1943.
In 1957, Frank Rosenblatt introduced the "perceptron".


---------------------









The goal of this article is to describe the mathematics of Neural Networks and
how to use this knowledge to build one from scratch using python.

You can find the python code in [this jupyter notebook](https://github.com/GarreauArthur/ldl/blob/master/NNfromScratch.ipynb)

### prerequisites

To be able to understand this article you should know about :

* Basic addition and multiplication
* Vectors
* Matrices (multiplication of two matrices, transpose)
* Linear Algebra (derivatives, and partial derivates)

### introduction

Nowadays any developer can build and train a (deep) neural network using a high
level API like tensorflow's keras. However, in order to get good results, you
should deeply understand the underlying mechanisms.

## A neuron

A single neuron is a computational unit. It takes any number of inputs and
output a single value. When given inputs, a neuron does 3 operations :

1. It multiplies the inputs by weights
2. It adds the weighted inputs and adds a biais term
3. It gives the result to an activation function and outputs a single value

The first two operations can be resume to compute z :

$$
z = \sum_{i=1}^{n} w_{i}x_{i} + b
$$

Then you gave z to a function called the activation function of the neuron :

$$
a = f(z)
$$

When picking an activation function, you want this function to be non-linear, 
monotonic, and continously differentiable.

Non-linearity is required, perceptron use linear

### bibliography

http://web.mit.edu/course/other/i2course/www/vision_and_learning/perceptron_notes.pdf



---
title: "The truth about perceptrons"
description: "What the hell is a perceptron"
layout: post
math: true
tags:
  - machine learning
  - deep learning
  - neural networks
comments: true
---

source : <https://blogs.umass.edu/brain-wars/files/2016/03/rosenblatt-1957.pdf>
<https://www.cs.cmu.edu/afs/cs.cmu.edu/academic/class/15381-f01/www/handouts/110601.pdf>
<http://www.cs.princeton.edu/~tcm3/docs/mapl_2017.pdf>

Percetron was first referenced in 1957 by Frank Rosenblatt. Rosenblatt focused
his attention on the feasibility of constructing a device possessing perception
and recognition abilities.

A perceptron is a system able to learn to recognize similarities or identities
between patterns of optical, electrical or tonal information, in a manner which
may be closely analogous to the perceptual processes of a biological brain. The
proposed system depends on probabilistic rather than deterministic principles
for its operation, and gains its reliability from the properties of statistical
measurements obtained from large populations of elements.

A system which operates according to these principles will be called a
perceptron.


In 1962

A perceptron is first and foremost a brain model, not an invention for pattern
recognition... its utility is in enabling us to determine the physical
conditions for the emergence of various psychological properties.
