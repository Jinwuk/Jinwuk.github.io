---
layout: post
title:  "Weak solution of Stochastic Differential Equation"
date:   2019-01-29 01:45:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
  - Geometrical SDE
comments: true
---

* Table of Contents
{:toc}

Fokker-Plank 방정식을 만족하는 probablity density 를 가진 diffusion process가 어떤 stochastic differential equation의 해 인 경우를 생각해보자.  이는 stochastic differential equation의 weak solution과 깊이 연관되어 있다.

## Concept of weak solution 
Let the stochastic differential equation as follows:

$$
dX_t = a(t, X_t)dt + b(t, X_t)dW_t
\label{eq01:concept}
\tag{1}
$$

with the initial value $X_{t_0} = Y_{t_0}$ for any Wiener process $W = \{ W_t, t \geq 0 \}$.
이때, coefficients는 strong solution을 만족한다고 가정하자 (Measurability, Lipschitz continuous, linear growth, Strong solution theorem). 그러면, for each Wiener process, there will be a solution $X$. 

이러한 Solution $X​$는 the given diffusion process $Y​$에 대해 동등한 stochastic process이다. 그리고 **$X​$와 $Y​$의  probablity law는 같다.**
그러나 일반적으로는 **$X​$와 $Y​$의 Sample Path는 다르다. **

따라서, **위의 특성을 만족할 수 있는 Wiener process를 만드는 것이 목표**가 된다.

Let $Y$ be a given difussion process on $[0, T]$ with **drift $a(t, y)$** and **strictly positive diffusion coefficient $b(t, y)​$** 

We define functions $g$ and $\bar{a}​$ by

$$
g(t,y) = \int_0^y \frac{1}{b(t,x)} dx
\label{eq02:concept}
\tag{2}
$$

and

$$
\bar{a}(t,x) = \left( \frac{\partial g}{\partial t} + a \frac{\partial g}{\partial y} + \frac{1}{2} b^2 \frac{\partial^2 g}{\partial y^2} \right)(t, g^{-1}(t, z))
$$

- $\eqref{eq01:concept}​$ 와 같이 한 이유는 

$$
dg(t, y) = \frac{1}{b(t, x)} dx \biggr\vert_{x = y} \Rightarrow \frac{dg}{dy}(t, y) = \frac{1}{b(t, x)}
$$

가 되도록 하여 diffusion coefficient가 1이 되도록 하기 위함이다.

Let $y = g^{-1}(t,z)$ is the inverse of $z = g(t, y)$.
Then, we define a process
$$
Z_t = g(t, Y_t)
$$

which is a diffusion procerss with **drift $\bar{a}(t,z)$** and **diffusion coefficient 1** such that, 

$$
dZ_t = \frac{\partial g}{\partial t}dt + \frac{\partial g}{\partial y}dY_t + \frac{1}{2}\frac{\partial^2 g}{\partial y^2}(dY_t)^2.
$$

Since $Y_t$ includes a drift $a(t, y)$ and diffusion coefficient $b(t, y)$, i.e.

$$
dY_t = a(t, y) dt + b(t, y)dW_t
$$


$$
dZ_t = \left( \frac{\partial g}{\partial t} + a\frac{\partial g}{\partial y} + \frac{1}{2} b^2  \frac{\partial^2 g}{\partial y^2} \right) (t, y) dt+ b\frac{\partial g}{\partial y} (t, y) dW_t
\label{eq03:concept}
\tag{3}
$$

and a process.

$$
\tilde{W}_t = Z_t - Z_0 - \int_0^t \bar{a} (S, Z_s) ds 
\label{eq04:concept}
\tag{4}
$$

which will  turn out to be a **Wiener process. ** (It reuires proof). 

Consequently, $\eqref{eq04:concept}​$ will be equivalent to the stochastic differential equation

$$
dZ_t = \bar{a}(t, Z_t)dt + 1 d\bar{W}_t
$$
