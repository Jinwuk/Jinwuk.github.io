---
layout: post
title:  "Existence and Uniquness of Stochastic Differential Equation"
date:   2018-12-06 01:45:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
  - Geometrical SDE
comments: true
---

* Table of Contents
{:toc}

This article illustrates the existance and uniqiness of stochastic differential equiations.  In the procesudre of the proof, there are many techniques and ideas for the analysis of the dynamics described by a stochastic  differential form. Most of contents in this articles are strongly depndeing on the reference[1].

## Strong Solution
Let the stochastic differential equation as follows:

$$
dX_t = a(t, X_t) dt + b(t, X_t)dW_t
\label{eq01:strong}
$$

The integral form of  $$\eqref{eq01:strong}$$ is

$$
X_t = X_{t_0} + \int_{t_0}^t a(s, X_s)ds + \int_{t_0}^t b(S, X_s) dW_s
\label{eq02:strong}
$$

### Lemma : Uniqueness
If assumptions of the measurablity and Lipschitz continuous in [Important Assumption and Lemma for Stochastic Analysis](https://jinwuk.github.io/mathematics/stochastic%20calculus/2018/11/25/Stochastic-Calculus-Important_Assumption_and_Lemma.html#borel-cantelli-lemma) are hold, then the solution of $$\eqref{eq02:strong}$$ corresponding to **the same initial value and the same Wiener process are pathwise unique.**

#### proof of Lemma


### Theorem : Strong Solution
Under assumptions in the article, [Important Assumption and Lemma for Stochastic Analysis](https://jinwuk.github.io/mathematics/stochastic%20calculus/2018/11/25/Stochastic-Calculus-Important_Assumption_and_Lemma.html#borel-cantelli-lemma), the stochastic differential equation $$\eqref{eq01:strong}$$ has a pathwise unique strong solution $$X_t$$ on $$[t_0, T]$$ with 

$$
\sup_{t_0 \leq t \leq T} \mathbb{E} \left( |X_t |^2 \right) < \infty
$$

#### proof
Let $$X_t^{(0)} \equiv X_{t_0}$$ and

$$
X_t^{(n+1)} = X_{t_0} + \int_{t_0}^t a(s, X_s^{(n)})ds + \int_{t_0}^t b(S, X_s^{(n)}) dW_s
\label{eq01:strong_pf}
$$

for $$n = 0, 1, 2, \cdots $$.

For assumption of the initial value, it is clear that

$$
\sup_{t_0 \leq t \leq T} E\left( |X_t^{(0)} |^2 \right) < \infty
$$

Applying the inequality $$(a + b +c)^2 \leq 3(a^2 + b^2 + c^2)$$, the Cauchy-Schwarz inequality and the linear growth bound to $$\eqref{eq01:strong_pf}$$, 

**Note 1**
By the Cauchy-Schwartz inequality,
$$
\begin{aligned}
\left| \int_{t_0}^T A(s) ds \right|^2 

&\leq \int_{t_0}^T \left| A(s) \right| ds \cdot \int_{t_0}^T \left| A(s) \right| ds \\

&\leq \int_{t_0}^T \left| A(s) \right|^2 ds \cdot \int_{t_0}^T  ds 
\;\;\; \because |a|^2 \leq |A|^3
\end{aligned}
$$

Therefore,

$$
\left| \int_{t_0}^T A(s) ds \right|^2 = (T - t_0) \int_{t_0}^T \left| A(s) \right|^2 ds
$$
**End of Note 1**


we obtain
$$
\begin{aligned}
\mathbb{E} \left( \left| X_t^{(n+1)} \right|^2 \right)

&\leq 3 \mathbb{E} \left( \left| X_{t_0} \right|^2 \right) + 3 \mathbb{E} \left( \left| \int_{t_0}^t a(s, X_s^{(n)}) ds \right|^2 \right) + 3 \mathbb{E} \left( \left| \int_{t_0}^t b(S, X_s^{(n)}) dW_s \right|^2 \right)  \\

&\leq 3 \mathbb{E} \left( \left| X_{t_0} \right|^2 \right) + 3 (T - t_0) \mathbb{E} \left(  \int_{t_0}^t \left| a(s, X_s^{(n)}) \right|^2 ds  \right) + 3 \mathbb{E} \left( \int_{t_0}^t \left| b(S, X_s^{(n)}) \right|^2 d_s  \right) \\

&\leq 3 \mathbb{E} \left( \left| X_{t_0} \right|^2 \right) + 3 (T - t_0 + 1) K^2 \mathbb{E} \left( \int_{t_0}^t \left( 1 + \left| X_s^{(n)} \right|^2 \right) d_s  \right)

\end{aligned}
$$

for $$n=0, 1, 2, \cdots $$. By induction we thus have

$$
\sup_{t_0 \leq t \leq T} \mathbb{E} \left( \left| X_t^{(n)} \right|^2\right) \leq C_0 < \infty
$$

for $$n=0, 1, 2, \cdots $$.














## References
[1]

~~~bibtex
@book{kloeden2011numerical,
  title={Numerical Solution of Stochastic Differential Equations},
  author={Kloeden, P.E. and Platen, E.},
  isbn={9783540540625},
  lccn={92015916},
  series={Stochastic Modelling and Applied Probability},
  url={https://books.google.co.kr/books?id=BCvtssom1CMC},
  year={2011},
  publisher={Springer Berlin Heidelberg}
}
~~~