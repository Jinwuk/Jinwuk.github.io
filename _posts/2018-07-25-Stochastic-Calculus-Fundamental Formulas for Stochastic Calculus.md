---
layout: post
title:  "Fundamental Formulas for Stochastic Calculus "
date:   2018-07-25 17:39:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
comments: true
---

* Table of Contents
{:toc}

## Diffusioin Process

#### Stochastic Differential Equation

$$
dX_t = \mu(X_t, t)dt + \sigma(X_t, t) dW_t
$$

#### Differential Operator 

$$
\mathscr{L}_t f(X_t, t) = (\mathscr{L}_t f)(X_t, t) 
= \frac{1}{2} \sigma^2 (X_t, t) \frac{\partial^2 f}{\partial x^2} (X_t, t) + \mu (X_t, t) \frac{\partial f}{\partial x}(X_t, t)
$$

#### Backward Equation

$$
\frac{\partial u}{\partial x}(x,s) + \mathscr{L}_t u(X_s, s) = 0
$$

#### Forward Equation

$$
-\frac{\partial p}{\partial t} + \frac{1}{2}\frac{\partial^2}{\partial x^2}(\sigma^2 (x,t)p) - \frac{\partial}{\partial x}(\mu(x,t)p) = 0
$$

#### Ito Equation

$$
df(X_t, t)=\left(\mathscr{L}_t f(X_t, t) + \frac{\partial f}{\partial t}(X_t, t) \right)dt + \sigma(X_t, t)\frac{\partial f}{\partial x}dW_t
$$


#### Dynkin's Formula

$$
Ef(X_t, t)=f(X_0, 0) + \int_0^t \left( \mathscr{L}_u f(X_u, u) + \frac{\partial f}{\partial t}(X_u, u) \right) du
$$

#### Corollary of Dynkin’s Formula (1)

$$
\begin{align*}
\mathscr{L}_t f(x,t) + \frac{\partial f}{\partial t}(x,t) = 0
\end{align*}
$$

#### Corollary of Dynkin’s Formula (2)

$$
\begin{align*}
\mathscr{L}_t f(x,t) + \frac{\partial f}{\partial t}(x,t) &= -\phi(x)\;\;\text{with }f(x,T)=g(x)\;\; \text{and }f(x) \text{ is solution where} \\
f(x, t)&=E(g(X_T)) + \int_t^T \phi(X_s) ds |_{X_t = x}
\end{align*}
$$

#### Feynmann-Kac Formula

$$
\begin{align*}
\mathscr{L}_t f(x, t) + \frac{\partial f}{\partial t}(x,t) &= r(x,t)f(x,t) \text{with}\;\; f(x,T)=g(x) \\
f(x,t) &= E\left( \exp(-\int_t^T r(X_u, u) du) g(X_T)|_{X(t)=x} \right)
\end{align*}
$$
