---
layout: post
title: "The Perceptron : a learning binary classifier [nn part 2]"
date: 2018-12-04
math: true
comments: true
tags:
  - machine learning
  - Mathematics
  - Neural network
  - perceptron
  - binary classifier
---

Plan, ici, je veux reprendre à partir du binary classifier, pour introduire le perceptron => apprentissage des paramètres w et b.

* [ ] repartir de l'équation préc
* [ ] this is pretty much the definition of a perceptron
* [ ] img graph
* [ ] a perceptron learns w and b
* [ ] perceptron is from the past
* [ ] mesure performance (error)
* [ ] learning algo (gradient descent)

perceptron -> neuron -> logistic regression (proba)

----

In this article I want to introduce historic models that led to the current artificial neurons. I am usually not a big fan of going through the history of
a technology just to learn the current one, but in the case of neural networks,
it is common to see record-breaking models built from old ideas.

In the previous article we ended up with the following formula :

$$y = \mathcal{H}(\mathbf{x} \cdot \mathbf{w}-b)$$

This is (almost) how Warren McCulloch and Walter Pitts proposed in 1943 a model of a neuron called a *Threshold Logic Unit*. (The original paper is pretty hard to read, I am not saying it, he does : http://www2.fiit.stuba.sk/~kvasnicka/Logika/Lecture08/Kvasnicka_Pospichal_SETINAIR%202013.pdf)

This classifier has two parameters **w** and *b*. Finding appropriate values to
them manually is pretty straightforward in up to 3-dimensional spaces. But it
gets harder when we want to have more features, and we don't want to do the hard work.

We can learn the values of **w** and *b*.

This is pretty much the modern definition of a "perceptron". I don't really like the name "perceptron" because its meaning can be confusing, and has evolved through the years.

Learning is all about making mistakes and correcting them to get better, right ?!

To learn we need a

----

What's a perceptron

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

----

Whatever, it may be incorrect, but let's stick with the name perceptron.

