je crois que l'algo de backprop a été une vraie révolution, ça serait pas mal
d'en parler

je pourrais peut être parler des algos de recherche/d'optimisation en général
aussi

des autres techniques

DL without backprop : https://iamtrask.github.io/2017/03/21/synthetic-gradients/



# chain rule

chain rule is easily understandable when written with the Liebniz notation

$$
\frac{\mathrm{d} f}{\mathrm{d} x} = \frac{\mathrm{d} f}{\mathrm{d} g} \cdot \frac{\mathrm{d} g}{\mathrm{d} x}
$$

But you may have already seen it with the Lagrange notation:

$$
(f \circ g)'(x)=(f' \circ g)(x)\cdot g'(x)
$$

or like this

$$
(f \circ g)'=(f' \circ g)\cdot g'
$$

or

$$
(f \circ g)'=g'(x)\cdot f'(g(x))
$$

Sometimes the Lagrange notation is called the Newton notation, there's even a
[meme](https://knowyourmeme.com/photos/1362046-american-chopper-argument) about
but it really is the Lagrange notation. But it doesn't matter because the
Liebniz notation is much better.

Fun fact : Liebniz made some cool work on logic, and wanted to build a machine
able to solve all problems using some sort of logical representation
En dire plus c'est intéressant
