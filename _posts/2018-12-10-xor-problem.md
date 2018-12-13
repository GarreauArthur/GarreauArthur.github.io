---
layout: post
title: "The nonlinearity problem : Mutlilayer Perceptron [nn part 3]"
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

Hello humans, by know you should know what the heck is a perceptron : a way to find the parameters **w** and *b* of a binary linear classifer. Recall that we will be using the following definition of a b.l.c :

$$y = \mathcal{H}(\mathbf{x} \cdot \mathbf{w}-b)$$

With a perceptron we can easily find appropriate value of *b* and **w** to compute many boolean functions. We can do it easily with the "OR" function :

$$
x_1\vee x_2 \text{ also noted } x_1 + x_2
$$

The "OR" function has the following truth table :

| x1 | x2 | x1 + x2 |
|----|----|---------|
| T  | T  | True    |
| T  | F  | True    |
| F  | T  | True    |
| F  | F  | False   |

If we plot these value, we can see that we can seperate them by a line :

![OR function](/img/nn/orBool.png)

By setting :

$$
\mathbf{w}=\begin{pmatrix}10\\10\end{pmatrix}\text{ and }b= 5
$$

we can implement this function using a perceptron.

Ok, nice, but what about the XOR function ?

| x1 | x2 | x1 xor x2 |
|----|----|-----------|
| T  | T  | False     |
| T  | F  | True      |
| F  | T  | True      |
| F  | F  | False     |

Try to seperate these points by a line...

![XOR function](/img/nn/xor.png)

Yep, you can't.

Let's try to be a little bit smart and go back to the definition of the "Xor" :

$$
x_1 \oplus  x_2 = (x_1 \wedge \neg x_2) \vee (\neg x_1 \wedge x_2)
$$

The xor function is made of 3 basic operations : one OR, and two ANDs. The two ANDs are really similar, let's call them "partial xor". If we focus on
one of them :

$$
\text{Partial xor = }x_1 \wedge \neg x_2
$$

We can write the truth table

| x1 | x2 | x1 Pxor x2 |
|----|----|------------|
| T  | T  | False      |
| T  | F  | True       |
| F  | T  | False      |
| F  | F  | False      |

If we plot it, we can see that we can seperate the true from the false by a line.

![partial xOR function](/img/nn/partialXor.png)

We can use a perceptron, if we set (for example) :

$$
\mathbf{w}=\begin{pmatrix}10\\-10\end{pmatrix}\text{ and }b= 5
$$

If we want to use the same weight vector to implement the second partial xor, we just need to switch the rows of *x1* and *x2* in **x** :

$$
\mathbf{x}=\begin{pmatrix}x_2\\x_1\end{pmatrix}
$$

Now that we have a way to represent these 3 operations with perceptrons. We can link them together.

![IMAGE TREE OPERATIONS](/img/nn/)


![IMAGE multi-layer PERCETRONS with weights](/img/nn/)


