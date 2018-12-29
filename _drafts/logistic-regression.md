---
layout: post
title: yeet
math: true

---

We can define learning as trying and minimizing the error between the experiment and reality


first trying, repeating by slightly modifying the way we work

## Learning.

Someone is smart when you can
the smarter you are, the less you need to repeat to understand and learn, and
get things right

## Measure performance

To be able to learn we need a way to measure how well or how bad we perform.
In pratice, we focus our attention on what went wrong, we measure an error. Our
goal will be to minimize the error.

We can just count the number of examples we got wrong over the number of all
examples : this is the classification error

Example we want to classify images of dogs and cats :

| examples | cat  | dog  | reality |
|----------|------|------|---------|
| 1        | 0.69 | 0.31 |  yes    |
| 2        | 0.42 | 0.58 |  no     |
| 3        | 0.31 | 0.69 |  yes    |
| 4        | 0.91 | 0.09 |  yes    |
| 5        | 0.49 | 0.51 |  yes    |
| 6        | 0.89 | 0.11 |  no     |

The classification error is equal to 2/6 or 1/3 (about 33%). It means that 33%
of the time the system fails to classify the images.

The problem of this method is that it doesn't give any idea of how wrong/right
we are. We would like to have a different measurement to say that our system performs
better when it gets it right with a probability of 99% rather than with 0.5001%.

With this metric we can't really do anything,

The Lp norm :

$$
\left \| L \right \|_p = \left ( \sum_{i} \left | L_i\right |^p\right  )^{\frac{1}{p}}
$$


### cross entropy

Let p<sub>reality</sub>(label) be the reality.
Let q(label|x,W,b) the learned probabilty distribution

| label | cat | dog |
|-------|-----|-----|
| p     | y   | 1-y |
| q     | ŷ   | 1-ŷ |

en fait je crois que j'ai du mal à faire la différence entre variable aléatoire
et la variable X

je suis très confu, parce que pour moi les événements sont :
* X est une image d'un chat : proba y
* X est une image d'un chien : proba 1-y

et donc X est un paramètre de la loi de distribution



## Maximum likelihood estimation

* [ ] prendre des notes à partir des vidéos
* [ ] adapter les notations
* [ ] adapter au problème

Let's say we have a population of dogs and cats. We take a sample of the
population of N examples and we want to estimate the probability *p* that an individual is a
cat. Because we only have dogs and cats, we can define a probability distribution
function which determines if an individual is a dog or cat :

$$
f(x_i| p) = p^{x_i}\cdot(1-p)^{1-x_i}
\\
\text{where }x_i = \left\{\begin{matrix}
 1, \text{if cat}\\ 
 0, \text{if dog}
\end{matrix}\right.
$$

For one example:

$$
f(1| p) = p^{1}\cdot(1-p)^{0} = p
\\
f(0| p) = p^{0}\cdot(1-p)^{1} = 1-p
$$

For N examples:

$$
f(x_1,x_2,...,x_N| p)=f(x_1| p)f(x_2| p)...f(x_N| p)
\\
\begin{align*}
f(x_1,x_2,...,x_N| p) &= \prod_{i=1}^{N}f(x_i| p) \\ 
 &= \prod_{i=1}^{N}p^{x_i}\cdot(1-p)^{1-x_i}
\end{align*}
$$

Inside the population there is a true but unknown probability \(p_data(x)\). We
are trying to come up with an estimator \(\hat{p}\)

The likelihood represents the probability that we would have got that sample of
individuals if we actually knew the probability p in the population. But we
don't know p and we try to estimate it.

$$
Likelihood =\prod_{i=1}^{N}p^{x_i}\cdot(1-p)^{1-x_i}
$$

we want to maximize the likelihood

$$
\frac{\partial L}{\partial p}=0 \Rightarrow \hat{p}_{ML}
$$

(ML stands for Maximum Likelihood)

To be able to compute the derivative, we transform this product into a sum, with
the log function :

$$
\begin{align*}
l &= log(\prod_{i=1}^{N}p^{x_i}\cdot(1-p)^{1-x_i})\\ 
 &=\sum_{i=1}^{N}log[p^{x_i}\cdot(1-p)^{1-x_i}]  \\ 
 &=\sum_{i=1}^{N} [ log(p^{x_i})+log((1-p)^{1-x_i}) ]\\ 
 &=\sum_{i=1}^{N} [ x_i \cdot log(p)+(1-x_i) \cdot log(1-p) ]\\
 &= log(p) \cdot \sum_{i=1}^{N}x_i + log(1-p) \sum_{i=1}^{N}(1-x_i)
\end{align*}
$$

We can even simplify this equation if we see that :

$$
\text{the mean of x} = \bar{x} = \frac{1}{N}\sum_{i=1}^{N}x_i
$$

$$
l = N \cdot \bar{x} \cdot log(p) + N \cdot (1-\bar{x})  \cdot log(1-p)
$$

Computing 

$$
\frac{\partial l}{\partial p}=0 \Rightarrow \hat{p}_{ML}
$$

is equivalent to computing without the log, because the logarithm is monotone

Now it's really simple to compute this equation (for the sake of clarity, I
don't use the subscript ML) :

$$
\frac{\partial l}{\partial \hat{p}} = \frac{N \cdot \bar{x}}{\hat{p}}-\frac{N \cdot (1-\bar{x})}{1-\hat{p}}=0
\\
\frac{N \cdot \bar{x}}{\hat{p}}=\frac{N \cdot (1-\bar{x})}{1-\hat{p}}
\\
\frac{\bar{x}}{\hat{p}}=\frac{(1-\bar{x})}{1-\hat{p}}
\\
\bar{x} \cdot (1-\hat{p}) = \hat{p} \cdot (1-\bar{x})
\\
\bar{x}-\bar{x}\hat{p} = \hat{p} -\bar{x}\hat{p}
\\
\bar{x}= \hat{p} 
$$

The maximum likelihood is equivalent to counting the number of cat in the
sample and dividing it by the total number of individual in the sample.

$$
\hat{p}_{ML}=\frac{1}{N}\sum_{i=1}^{N}x_i
$$

All of this just for that, yeet that was obvious.



-----------------------------

| x       | Cat         | Dog           | Reality (cat) |
|---------|-------------|---------------|---------------|
| x^{(1)} | \hat{y}^(1) | 1-\hat{y}^(1) | y^{(1)}       |
| x^{(2)} | \hat{y}^(2) | 1-\hat{y}^(2) | y^{(2)}       |
| ...     | ...         | ...           | ...           |
| x^{(N)} | \hat{y}^(N) | 1-\hat{y}^(N) | y^{(N)}       |


Our bet is that there is a function that maps any value of \(x^{(i)}\)  to
\(y^{(i)}\). We want to find it.

To do that we compute a probability mass function

-------------------------------------

Let's say that we have a sample of a population of images of cats and dogs :

$$
\mathbb{X} = \left \{ \left. x^{(1)}, x^{(2)}, ... , x^{(N)}\right \} \right.
$$

Each of these images has a label y = 1 if it's a cat, y = 1 if it's a dog.

$$
\mathbb{Y} = \left \{ \left. y^{(1)}, y^{(2)}, ... , y^{(N)}\right \} \right.
$$

What the neural network computes is really just a function that maps each \(x^{(i)}\)
to a probability \(\hat{y}^(i)\)

We can see the learning process as computing different probability distributions
over K classes :

$$
\sum_{j=1}^{K}\hat{y}^{(i)}_j=1
$$

Here K = 2 :

$$
\mathbf{\hat{y}^{(i)}} = \begin{pmatrix}
\hat{y}^{(i)}_1\\ 
\hat{y}^{(i)}_2
\end{pmatrix}= \begin{pmatrix}
\hat{y}^{(i)}\\ 
1-\hat{y}^{(i)}
\end{pmatrix}
$$



| X      | x is a cat  | x is a dog    | total |
|--------|-------------|---------------|-------|
| p(X=x) | \(\hat{y}\) | 1-\(\hat{y}\) | 1     |













### references/ressources/ideas

* C. Olah. 2015 October 14. Visual Information Theory. Colah's blog. <http://colah.github.io/posts/2015-09-Visual-Information/>
* <https://web.stanford.edu/class/archive/cs/cs109/cs109.1166/pdfs/41%20DeepLearning.pdf> 


