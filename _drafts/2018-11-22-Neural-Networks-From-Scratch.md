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

I made [this jupyter notebook](https://github.com/GarreauArthur/ldl/blob/master/NNfromScratch.ipynb)

I was about to write an article explaining how neural nets work, and how you can
implement one from scratch using python, to demonstrate my ability to communicate
on a complex subject. But <del>idk i feel like dying today</del> there are
already tons of ressources to learn about neural net, you don't need one more.




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