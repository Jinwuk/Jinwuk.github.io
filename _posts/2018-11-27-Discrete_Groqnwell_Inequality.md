---
layout: post
title:  "Discrete_Groqnwell_Inequality"
date:   2018-11-27 01:45:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
  - Geometrical SDE
comments: true
---

* Table of Contents
{:toc}

This article illustrates the Discrete Gronwall's Lemma and Applications [1].

## Introduction 
The most formidable case in a sequence analysis, we meet the following equations: to sum over n from$n=0$ to $n=N-1$ on the left and right hand sides of both

$$
\begin{aligned}
X_{n+1} - x_n &= F_n (X_n) \\
\bar{X}_{n+1} - \bar{x}_n &= F_n (\bar{X}_n) + \xi_n
\end{aligned}
$$

to obtain
$$
\bar{X}_N - X_N = \bar{X}_0 - X_0 + \sum_{n=0}^{N-1} \left( F_n(\bar{X}_n) - F_n (X_n) \right) + \sum_{n=0}^{N-1} \xi_n.
$$

Suppose that the function $F_n$ are Lipschitz continuous with Lipschitz constants $L_n > 0$, and set $\bar{X_0} = X_0$. We get

$$
\| \bar{X_N} - X_N \| \leq \| \sum_{n=0}^{N-1} \xi_n \| + \sum_{n=0}^{N-1} L_n \| \bar{X}_n - X_n \|
$$

and therein lies the problem.

이러한 경우에 대한 해석을 위해 Discrete Gronwell's Lemma가 필요하다. 

In [1], let $\{x_n\}_{n=0}^{\infty}$, $\{a_n\}_{n=0}^{\infty}$, and $\{b_n\}_{n=0}^{\infty}$ be sequences of real numbers, with the $b_n \geq 0$, which satisfy

$$
x_n \leq a_n + \sum_{j=n_0}^{n-1} b_j x_j n, \;\;  \in \mathbf{Z}[n_0, \infty]
\label{eq01:intro}
\tag{1}
$$

For any integer $N > n_0$ , let 

$$
S(n_0, N) = \{k \vert k = \arg \max \frac{x_k}{\prod_{j=n_0}^{k-1} (1+b_j)}, \; \forall n \in \mathbf{Z}[n_0, N]  \}
$$

Then, for any $\theta \in S(n_0, N)$,

$$
x_n \leq a_{\theta} \prod_{j=n_0}^{n-1} (1 + b_j), \;\; n \in \mathbf{Z}[n_0, N]
$$

In paticular, for $\bar{a}_{\theta} = \min a_{\theta} \prod_{j=n_0}^{n-1} (1 + b_j), \; \text{for } \theta \in S(n_0, N),\; n \in \mathbf{Z}[n_0, N] $,

$$
x_n = \bar{a}_{\theta} \prod_{j=n_0}^{n-1} (1 + b_j), \;\; n \in \mathbf{Z}[n_0, N]
$$

그러나,  2009년에 이것에서 더 발전된 형태의 Grownwell 부등식이 소개 되었다.  결론만 보면 방정식 $\eqref{eq01:intro}$ 와 같이 주어졌을 때

$$
x_n \leq a_n + \sum_{j=n_0}^{n-1} a_j b_j \exp (\sum_{j < k < n} b_k), \;\;  \in \mathbf{Z}[n_0, \infty]
$$

와 같다 [2].  이를 자세히 살펴본다.

## Fundamental Expressions of Gronwall's Lemma

### Gronwall's Lemma

Let $y(t)$, $f(t)$, and $g(t)$ be **nonnegative** functions on $\mathbf{R}[0, T]$ having one-sided limits at every $ t \mathbf{R}[0, T]$, and assume that for $0 \leq t \leq T​$ we have

$$
y(t) \leq f(t) + \int_0^t g(s) y(s)ds
$$

Then for $0 \leq t \leq T$ we also have

$$
y(t) \leq f(t) + \int_0^t g(s) f(s) \exp \left( \int_s^t g(u) du \right) ds
$$

In many cases, $g(\cdot)$ is Lipschitz constant, i.e. $g(\cdot)= L$, we obtain more abbreviate formulation such that

$$
y(t) \leq f(t) + L \int_0^t f(s) \exp (L(t - s))  ds
$$

### Discrete Gronwall inequality
If $\langle y_n \rangle$, $\langle f_n \rangle$, and $\langle g_n \rangle$ are nonnegative sequences and

$$
y_n \leq f_n + \sum_{0 \leq k \leq n} g_k y_k, \;\; \forall n \geq 0,
\label{eq01:DGI}
\tag{2}
$$

then

$$
y_n \leq f_n + \sum_{0 \leq k \leq n} f_k g_k \exp \left( \sum_{k<j<n} g_j \right), \;\; \forall n \geq 0,
\label{eq02:DGI}
\tag{3}
$$

이를 증명하기 위해 먼저 $f_n \equiv 1$ 인 경우에 대하여 생각한다.

### Lemma
Let $\langle g_n \rangle$ be a sequence. For $n \geq 0$ let

$$
G_n := \prod_{0 \leq j \leq n} (1 + g_j).
\label{eq01:lemma}
\tag{4}
$$

Then

$$
G_n = 1 + \sum_{0 \leq j \leq n} g_j G_j
\label{eq02:lemma}
\tag{5}
$$

for $n \geq 0$, and more generally, for $0 \leq k \leq n$ ,

$$
G_n = G_k + \sum_{k \leq j < n} g_j G_j
\label{eq03:lemma}
\tag{6}
$$

#### proof of lemma
Assume that, for $k < n$, the equation $\eqref{eq01:lemma}$ and $\eqref{eq02:lemma}$ are hold such that

$$
G_k = \prod_{0 \leq j \leq k} (1 + g_j), \;\;G_k = 1 + \sum_{l \leq j < k} g_j G_j
$$

For $k+1>k$

$$
G_{k+1} = \prod_{0 \leq j \leq k+1} (1 + g_j) = \prod_{0 \leq j \leq k} (1 + g_j) \cdot (1 + g_{k}) = G_k\cdot (1 + g_{k}) = G_k + g_{k} G_k
$$

Therefore,

$$
G_{k+1} = 1 + \sum_{l \leq j < k} g_j G_j + g_{k} G_k = 1 + \sum_{l \leq j < k+1} g_j G_j
$$

**Q.E.D.**

### Propostion
Assume that $\langle x_n \rangle$, $\langle f_n \rangle$, and $\langle g_n \rangle$ are nonnegative sequences and

$$
x_n = f_n + \sum_{0\leq k \leq n} g_k x_k, \; \text{for } n \geq 0
$$

Then

$$
x_n = f_n + \sum_{0\leq k \leq n} f_k g_k \prod_{k < j < n} (1+g_j)= f_n + \sum_{0\leq k \leq n} f_k g_k \frac{G_n}{G_{k+1}} , \; \text{for } n \geq 0 
\label{eq01:prop}
\tag{7}
$$

#### proof
- Idea (mainly from [1])

$$
\chi_n := f_n + \sum_{0\leq k < n} f_k g_k \frac{G_n}{G_{k+1}}
\label{eq02:prop}
\tag{8}
$$

- We shall prove that $x_m = \chi_m$ for $m \geq 0$.
- Since $G_{k+1} = G_k (1 + g_k)$,  

$$
G_{n} = G_{n-1} (1 + g_{n-1}) = G_{n-2} (1 + g_{n-1})(1 + g_{n-2}) = G_{k+1} \prod_{k < j < n} (1+g_j) \\
\therefore \prod_{k < j < n} (1+g_j) = G_n/G_{k+1}
$$

- In $\eqref{eq02:prop}$, $k = n-1$ 이면 $G_n/G_{n-1+1} = 1$, 고로 마지막 항은 $f_{n-1} g_{n-1}$.


For $n=0$, $x_0 = f_0 = \chi_0$, Assume that $x_n = \chi_n$ for $0 \leq n < m$. Then

$$
\begin{aligned}
x_m &= f_m + \sum_{0\leq k < m} g_k x_k = f_n + \sum_{0\leq k < n} g_k \chi_k \\

&= f_m + \sum_{0\leq k < m} g_k \left( f_k + \sum_{0\leq j < k} f_j g_j \frac{G_k}{G_{j+1}} \right) \\

&= f_m + \sum_{0\leq k < m} g_k f_k + \sum_{0\leq k < m} \sum_{0\leq j < k} g_k f_j g_j \frac{G_k}{G_{j+1}} \\

&= f_m + \sum_{0\leq k < m} g_k f_k + \sum_{0\leq j < m-1} \sum_{j \leq k < m} g_k f_j g_j \frac{G_k}{G_{j+1}} \\

&= f_m + \sum_{0\leq k < m} g_k f_k + \sum_{0\leq k < m-1} \sum_{k \leq j < m} g_j f_k g_k \frac{G_j}{G_{k+1}} \;\; \because \text j \leftrightarrow k \\

&= f_m + g_{m-1} f_{m-1} + \sum_{0\leq k < m-1} g_k f_k + \sum_{0\leq k < m-1} \sum_{k \leq j < m} g_j f_k g_k \frac{G_j}{G_{k+1}} \;\; \because \text j \leftrightarrow k \\

&= f_m + g_{m-1} f_{m-1} + \sum_{0\leq k < m-1} g_k f_k \left( 1 + \sum_{k \leq j < m} g_j \frac{G_j}{G_{k+1}} \right)\\

&= f_m + \sum_{0\leq k < m} g_k f_k \frac{G_m}{G_{k+1}} \;\; \because \text{by }\eqref{eq01:prop}, \eqref{eq02:prop} \\

&= \chi_m
\end{aligned}
$$

- No $k < j$ so that $\sum_{0\leq k < m} \sum_{0\leq j < k} = \sum_{0\leq j < m-1} \sum_{j \leq k < m}$. It is trivial

Consequently, $x_n = \chi_n$. 

**Q.E.D**

### Corollary
Therefore, instaed of $x_n$, there exists $y_n$ such that

$$
y_n \leq f_n + \sum_{0\leq k \leq n} g_k y_k, \; \text{for } n \geq 0
$$

Then

$$
y_n \leq f_n + \sum_{0\leq k \leq n} f_k g_k \prod_{k < j < n} (1+g_j) \; \text{for } n \geq 0 
\label{eq01:col}
\tag{9}
$$

#### Main proof of Discrete Gronwall's Lemma

Since 

$$
(1+g_j) \leq \exp(g_j),
$$

the mutiple production of $(1+g_j)$ in $\eqref{eq01:col}$ is replaced with $\exp$ such that

$$
\begin{aligned}
y_n &\leq f_n + \sum_{0 \leq k \leq n} f_k g_k \prod_{k < j < n}(1 + g_j )\\
&\leq f_n + \sum{0 \leq k \leq n} f_k g_k \exp(\sum_{k < j < n} g_j)
\end{aligned}
\label{eq01:main}
\tag{10}
$$

The equation $\eqref{eq01:main}$ is what we want.

### Case of Lipschitz Constants
In many cases, the $g_j$ is not a function but is a constant such as Lipschitz constants.
When we replaced $gj$ to a positive constant $L$, we can obtain the following Gronwall's inequality.

$$
\begin{aligned}
y_n
&\leq f_n + \sum{0 \leq k \leq n} f_k L \exp(\sum_{k < j < n} L) \\
&\leq f_n + L \sum{0 \leq k \leq n} f_k \exp(L(n-k)) \\
\end{aligned}
$$


## References

[1]

~~~bibtex
@article{CLARK1987279, 
title = "Short proof of a discrete gronwall inequality", 
journal = "Discrete Applied Mathematics", 
volume = "16", 
number = "3", 
pages = "279 - 281", 
year = "1987", 
issn = "0166-218X", 
doi = "https://doi.org/10.1016/0166-218X(87)90064-3", 
url = "http://www.sciencedirect.com/science/article/pii/0166218X87900643", 
author = "Dean S Clark", 
abstract = "We give an elementary proof of a generalization of the classical discrete Gronwall inequality xn⩽an + ∑j = n0n − 1bjxj, n = n0,…,N, implies xn⩽a∗ ∏j = n0n −1 (1+bj)a∗ = max{aj : j = n0,…,N}, n = n0,…,N) which improves the description of the multiplier a∗ to a minimum, rather than a maximum, over a certain subset of indices in {n0,…,N}." 
}
~~~

[2]
~~~bibtex
@INPROCEEDINGS{Holte2009, 
booktitle={MAA-NCS Meeting at the University of North Dakota}
title = {Discrete Gronwall Lemma and Applications}, 
year = {2009}, 
month={Oct},
url = {http://homepages.gac.edu/~holte/publications/GronwallLemma.pdf}, 
author = {J.M. Holte}, 
} 
~~~

