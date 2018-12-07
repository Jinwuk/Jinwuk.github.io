---
layout: post
title:  "Existence and Uniqueness of Stochastic Differential Equation"
date:   2018-12-06 01:45:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
  - Geometrical SDE
comments: true
---

* Table of Contents
{:toc}

This article illustrates the existence and uniqueness of stochastic differential equations.  In the procedure of the proof, there are many techniques and ideas for the analysis of the dynamics described by a stochastic  differential form. Most of contents in this articles are strongly depending on the reference[1].

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
If assumptions of the measurable and Lipschitz continuous in [Important Assumption and Lemma for Stochastic Analysis](https://jinwuk.github.io/mathematics/stochastic%20calculus/2018/11/25/Stochastic-Calculus-Important_Assumption_and_Lemma.html#borel-cantelli-lemma) are hold, then the solution of $$\eqref{eq02:strong}$$ corresponding to **the same initial value and the same Wiener process are path-wise unique.**

#### proof of Lemma

For $$N>0$$ and $$t \in [t_0, T]$$, we define the indication function such that

$$
I_t^{(N)}(w) = 
\begin{cases}
1 &: |X_u(w)|, |\tilde{X}_u(w)| \leq N \;\; \text{for} t_0 \leq u \leq t \\
0 &: \text{otherwise}
\end{cases}
$$

Obviously $$I_t^{(N)}$$ is $$\mathcal{A}_t$$-measurable and $$I_t^{(N)} = I_t^{(N)} I_s^{(N)}$$ for $$t_0 \leq u \leq t​$$.

Let $$Z_t^{(N)} = I_t^{(N)} (X_t - \tilde{X}_t)$$

$$
Z_t^{(N)} 
= I_t^{(N)} \int_{t_0}^t I_s^{(N)} \left( a(s, X_s) - a (s, \tilde{X}_s) ds \right) 
+ I_t^{(N)} \int_{t_0}^t I_s^{(N)} \left( b(s, X_s) - b(s, \tilde{X}_s) dW_s \right)
$$

By the Lipschitz condition, for $$t_0 \leq s \leq t$$,

$$
\max \left\{ \left| a(s, X_s) - a(s, \tilde{X}_s)\right|, \left| b(s, X_s) - b(s, \tilde{X}_s) \right| \right\}

\leq K I_s^{(N)} \left| X_s - \tilde{X}_s \right| \leq 2KN
\label{eq01:pf_lemma}
$$

Thus the following inequality is evaluated (and see the **Note 1**)

$$
\begin{aligned}
\mathbb{E} \left( \left| Z_t^{(N)} \right|^2 \right)

&\leq  2 \mathbb{E} \left( \left| \int_{t_0}^t I_s^{(N)} \left( a(s, X_s) - a(s, \tilde{X}_s) \right) ds \right|^2 \right) \\

&+ 2 \mathbb{E} \left( \left| \int_{t_0}^t I_s^{(N)} \left( b(s, X_s) - b(s, \tilde{X}_s) \right) dW_s \right|^2 \right) \\

&\leq  2 (T - t_0) \int_{t_0}^t \mathbb{E} \left( \left| I_s^{(N)} \left( a(s, X_s) - a(s, \tilde{X}_s) \right) \right|^2 \right) ds \\

&+ 2\int_{t_0}^t \mathbb{E} \left( \left| \left( b(s, X_s) - b(s, \tilde{X}_s) \right) \right|^2 \right) ds \;\;\; \because \text{Note 1} \\

&\leq  2 (T - t_0) K^2 \int_{t_0}^t \mathbb{E} \left( I_s^{(N)} \left| X_s - \tilde{X}_s \right|^2 \right) ds \\

&+ 2 K^2 \int_{t_0}^t \mathbb{E} \left( I_s^{(N)} \left| X_s - \tilde{X}_s \right|^2 \right) ds \;\;\; \because \text{By Lipschitz conditiion } \eqref{eq01:pf_lemma} \\

&\leq  2 (T - t_0 + 1) K^2 \int_{t_0}^t \mathbb{E} \left( I_s^{(N)} \left| X_s - \tilde{X}_s \right|^2 \right) ds 

\end{aligned}
$$

Therefore, we can obtain 

$$
\mathbb{E} \left( \left| Z_t^{(N)} \right|^2 \right) \leq L \int_{t_0}^t \mathbb{E} \left( \left| Z_s^{(N)}  \right|^2 \right)
$$

for $$ t \in [t_0, T]$$ where $$L = 2(T - t_0 + 1)K^2 $$.

Apply **Grownwall's Lemma** with $$\alpha(t) = \mathbb{E}\left( \left| Z_t^{(N)} \right|^2 \right)​$$ and $$\beta(t) \equiv 0$$, then

$$
\alpha(t) \leq \beta(t) + L \int_{t_0}^t e^{L(t-s)}\beta(s) ds
= 0.
$$

We conclude that

$$
\mathbb{E} \left( \left| Z_t^{(N)} \right|^2 \right) 
= \mathbb{E} \left( \left| I_t^{(N)} (X_t - \tilde{X}_t) \right|^2 \right) = 0.
$$

In addition, for $$t \in [t_0, T]$$, $$I_t^{(N)} X_t = I_t^{(N)} \tilde{X}_t$$ with probability 1.

Since **the sample paths are continuous almost surely**, they are bounded almost surely. Thus we can make the probability

$$
P \left( I_t^{(N)} \not\equiv 1, \forall t \in [t_0, T] \right) \leq P \left( \sup_{t_0 \leq t \leq T} |X_t| > N \right) + P \left( \sup_{t_0 \leq t \leq T} |\tilde{X}_t| > N \right)
$$

arbitrarily small by taking $$N$$ sufficiently large. This means that $$P \left( X_t \neq \tilde{X}_t \right) = 0$$ for each $$t \in [t_0, T] $$, and hence that $$P \left( X_t \neq \tilde{X}_t : t \in D \right) = 0$$ for any countable dense subset $$D$$ of $$[t_0, T]$$.

**Q.E.D**



### Theorem : Strong Solution

Under assumptions in the article, [Important Assumption and Lemma for Stochastic Analysis](https://jinwuk.github.io/mathematics/stochastic%20calculus/2018/11/25/Stochastic-Calculus-Important_Assumption_and_Lemma.html#borel-cantelli-lemma), the stochastic differential equation $$\eqref{eq01:strong}$$ has a path-wise unique strong solution $$X_t$$ on $$[t_0, T]$$ with 

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

이로써 **$$\mathbb{E} \left( \left| X_t^{(n+1)} \right|^2 \right)$$의 Finite 특성이 증명**되었음. 이를 토대로 **Lemma를 적용**한다.












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