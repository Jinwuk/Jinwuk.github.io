Maximization by Quadratic Hill-Climbing
====
This article is summarized of the paper, the name is "Maximization by Quadratic Hill-Climbing"[1]. It was illustrate firstly a crucial methodology to search the global minima with a quadratic algebra. The method proposed in this paper is known as the rank-1 method in the Quasi-Newton method. This article is written with English and Korean language, but it is somewhat difficult to read and understand whole of the article owing to the difference of language, so that I suppose that the reader who want to understand key idea of this article read the original paper. 

## Alternative Gradient method 

Let a function $f(x) : \mathbf{R}^n \rightarrow \mathbf{R}$ for $x \in \mathbf{R}^n$.
In addition, Let $H(x) \in \mathbf{R}^{n \times n}$ be the symmetric $n \times n$ Hessian matrix of $f(x)$. 

Choose a starting point $x^o$ and 

$$
x_{p+1} = x_p + h_p D_p
$$

where $h_p$ is a positive constant and $D_p \in \mathbf{R}^n$ is a direction vector.

The **Gradinet Method** iss that the choice of $D_p$ is given by

$$
D_p = B^{-1} \nabla f(x_p)
$$

where $B$ is a positive definite weighting matrix.

### The method of Steepest Ascent

A simple choice if $B$, suggested by Cauchy, is given by $B = I$.

Assume that a second order Taylor series expansion around $a \in \mathbf{R}^n$ is

$$
f(x) \approx f(a) + \langle \nabla f(a), x-a \rangle + \frac{1}{2} \langle x - a, H(a) (x - a) \rangle

\tag{1}
$$

Corresponding to (1), 식 (1)을 $x$에 대하여 Differentiating 하면

$$
\nabla f(x) \approx \nabla f(a) + H(a)(x - a)
$$

Since the steepest ascent method imples 

$$
x_{p+1} = x_p + h_p \nabla f(x_p) \Rightarrow x_{p+1} - x_p = h_p \nabla f(x_p) 

\tag{2}
$$

식 (2)를 식 (1)에 대입하고 $a$를 $x_p$로 바꾸면
Substitute (2) into (1), replacing $a$ by $x_p$, we obtain

$$
f(x_{p+1}) -f(x_p) = h_p \langle \nabla f(x_p), \nabla f(x_p) \rangle + \frac{1}{2} h_p^2 \langle \nabla f(x_p), H(x_p) \nabla f(X_p) \rangle

\tag{3}
$$

식 (3)에서 Let $G(h_p) = f(x_{p+1}) -f(x_p)$ 로 놓자. 그 경우, 이것을 극대/국소로 만들 수 있는 $h_p$를 생각해보면 그것은 $\frac{\partial G}{\partial h_p} = 0$ 이므로 

$$
\frac{\partial G}{\partial h_p} = \langle \nabla f(x_p), \nabla f(x_p) \rangle + h_p \langle \nabla f(x_p), H(x_p) \nabla f(X_p) \rangle = 0
$$

or 

$$
h_p = - \frac{\langle \nabla f(x_p), \nabla f(x_p) \rangle}{\langle \nabla f(x_p), H(x_p) \nabla f(X_p) \rangle}
$$

위에서 언급한 최적의 Step Size $h_p$가 Maximum을 얻게 하려면
The optimal step size $h_p$ yields a maximum we further require 

$$
\frac{\partial^2 G}{\partial h_p^2} = \langle \nabla f(x_p), H(x_p) \nabla f(X_p) \rangle < 0
$$

which is necessarily so if $H(x_p)$ is negative definite.

반대의 경우는 

$$
\frac{\partial^2 G}{\partial h_p^2} = \langle \nabla f(x_p), H(x_p) \nabla f(X_p) \rangle > 0
$$

$H(x_p)$ 가 Positive definite 이어야 한다.

- 실제로 이러한  optimal $h_p$는 잘 작동하지 못한다. 
- 따라서 이것보다는 어떤 대안들이 많이 제시 되며, 또한 그것들이 오히려 더 잘 작동한다.
- 실제로는 Maximum (Ascent)/Minimum(Descent) 보다는 Saddle point에 더 잘 수렴하며
- Maximum/Minimum가 narrow ridge/valley 에 있으면 go forward/backward의 반복으로 수렴에 많은 시간이 걸린다.

### Newton's Method




## Reference
~~~bibtex
@book{hillclimbing,
  abstract = {The purpose of this paper is to describe a new gradient method for
	maximizing general functions. After a brief discussion of various
	known gradient methods the mathematical foundation is laid for the
	new algorithm which rests on maximizing a quadratic approximation
	to the function on a suitably chosen spherical region. The method
	requires no assumptions about the concavity of the function to be
	maximized and automatically modifies the step size in the lifet of
	the success of the quadratic approximation to the function. The paper
	further discusses some practical problems of implementing the algorithm
	and presents recent computational experience with it.},
  added-at = {2012-12-29T01:24:39.000+0100},
  author = {Goldfeld, Stephen M. and Quandt, Richard E. and Trotter, Hale F.},
  biburl = {https://www.bibsonomy.org/bibtex/29a01d0629d93a430b8f61d5425b585b3/chsivic},
  copyright = {Copyright � 1966 The Econometric Society},
  interhash = {68db16b895a8cf452be3c6b08251e704},
  intrahash = {9a01d0629d93a430b8f61d5425b585b3},
  issn = {00129682},
  journal = {Econometrica},
  jstor_articletype = {primary_article},
  jstor_formatteddate = {Jul., 1966},
  keywords = {imported},
  number = 3,
  owner = {chensi},
  pages = {541--551},
  publisher = {The Econometric Society},
  timestamp = {2012-12-29T01:24:50.000+0100},
  title = {Maximization by Quadratic Hill-Climbing},
  url = {http://www.jstor.org/stable/1909768},
  volume = 34,
  year = 1966
}
~~~
