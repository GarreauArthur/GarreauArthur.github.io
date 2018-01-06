---
title: "Mathjax is now supported"
layout: post
math: true
comments: true
---

The tex2jax preprocessor defines the LaTex math delimiters, which are
`\\(...\\)` for in-line math and `\\[...\\]` for displayed equations. It also
defines the TeX delimiters `$$...$$` for displayed equations, but it does not
define `$...$` as in-line math delimiters. We can change that, but I don't want
to, because they had a reason to do so, and I think it easy to understand
what is it.

I like to use [this tool](https://www.codecogs.com/latex/eqneditor.php) to help me write LaTex expressions.

Very nice, let's try this 


	\\[\frac{10^{120}}{10^{106}} = 10^{120-106} = 10^{14}\\]

\\[\frac{10^{120}}{10^{106}} = 10^{120-106} = 10^{14}\\]

Volume of a ball

	$$\int_{\varphi=0}^{\pi}\int_{\theta = 0}^{2\pi}\int_{r=0}^{R}r^2\cdot\sin{\phi}\cdot d r \cdot d \phi \cdot d \theta = \frac{4}{3} \pi R^3$$

$$\int_{\varphi=0}^{\pi}\int_{\theta = 0}^{2\pi}\int_{r=0}^{R}r^2\cdot\sin{\phi}\cdot d r \cdot d \phi \cdot d \theta = \frac{4}{3} \pi R^3$$


Let's say we want to add a little bit of inline math

## Support Vector Machine

We try to separate positive from negative examples.

	^
	|\  \     +
	| \  \
	|  \  \ +  +
	| - \  \   + +
	|- - \  \ + 
	| - - \  \ +
	|______\__\_________




Let \\(\mathbf{w}\\) be a normal vector of the street, and \\(\mathbf{x}\\) a vector pointing to a sample. If we project \\(\mathbf{x}\\) on \\(\mathbf{w}\\), we obtain the scalar : 

\\[p = \frac{\mathbf{x} \cdot \mathbf{w}}{\|\| \mathbf{w} \|\|} = \|\| \mathbf{x} \|\| \cdot \cos(\mathbf{x},\mathbf{w})\\]

\\(\mathbf{w}\\) is always the same, so its norm \\(\|\| \mathbf{w} \|\|\\) is constant. So our problem can be written as :

$$\mathbf{x} \cdot \mathbf{w} \geqslant C$$

If \\(\mathbf{x} \cdot \mathbf{w} \geqslant C\\) where is C is a constant then the sample x is a positive element, otherwise, it is a negative one. If we let b = -C, we can rewrite this :

$$\mathbf{x} \cdot \mathbf{w} + b \geqslant 0$$

This is what we call the DECISION RULE. 

$$
\begin{align*}
 \mathbf{w} \cdot \mathbf{x_+} + b \geqslant 1 \\ 
 \mathbf{w} \cdot \mathbf{x_-} + b \leqslant -1
\end{align*}
$$
