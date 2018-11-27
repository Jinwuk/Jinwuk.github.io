---
layout: post
title:  "Important Assumption and Lemma for Stochastic Analysis"
date:   2018-11-26 01:45:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
  - Geometrical SDE
comments: true
---

* Table of Contents
{:toc}

This article illustrates fundamental assumptions and very useful lemmas for the stochastic analysis. Mainly, these are from the following reference [1].

## Destination Equation
Let the following non-autonomous scalar stochastic differential equation. It is slightly more general form.

$$
dX_t = a(t, X_t)dt + b(t, X_t) dW_t
\label{eq01:DE}
\tag{1}
$$
where $W_t$ is the Wiener process $W=\{W_t, t \geq 0 \}$, that is $\mathcal{F}^*$ adapted process.
each $t \in [t_0, T]$ 

Suppose that there are two solution $X_t$ and $\tilde{X}_t$ of the equation $\eqref{eq01:DE}$ and the solutions  are  **Path-wise unique** almost surely on the same sample path on $[t_0, T]$ such that

$$
P\left( \sup_{t_0 \leq t \leq T} \| X_t -\tilde{X}_t \| > 0 \right) = 0,
$$


## Fundamental Assumption
### Measurability
$a = a(t, x)$, and $b = b(t,x)$ are jointly ($\mathcal{L}^2 -$ ) measurable in $(t,x) \in [t_0, T] \times \mathbf{R}$; 

- $\mathcal{L}^2 $ means that the function is **the squared Lebsegue measurable**.

### Lipschitz condition
There exists a constant $K > 0$ such that

$$
\begin{aligned}
\| a( t,x) - a (t, y) \| \leq K \| x - y\| \\
\| b( t,x) - b (t, y) \| \leq K \| x - y\| 
\end{aligned}
$$

for all $t \in [t_0. T]$ and $x, y \in \mathbf{R}$;

### Linear growth bound
There exists a constant $K > 0$ such that

$$
\begin{aligned}
\| a(t,x) \|^2 \leq K^2 (1 + \| x \|^2) \\
\| b(t,x) \|^2 \leq K^2 (1 + \| x \|^2) 
\end{aligned}
$$

for all $t \in [t_0, T]$ and $x, y \in \mathbf{R}$

### Initial value 
$X_{t_{0}}$ is $\mathcal{F}_{t_0} $ measurable with $\mathbb{E}( \|X_{t_0} \|^2) < \infty$.

## Lemma
### Grownwall Inequality
Let $\alpha, \beta : [t_0, T] \rightarrow \mathbf{R}$ be integrable with

$$
0 \leq \alpha(t) \leq \beta(t) + L \int_{t_0}^t \alpha(s) ds 
$$

for $t \in [t_0, T]$ where $L > 0$ . Then

$$
\alpha(t) \leq \beta(t) + L \int_{t_0}^t e^{L(t-s)}\beta(s) ds
\label{eq01:lemma}
\tag{2}
$$

### Simple Version
Let $\alpha, \beta : [t_0, T] \rightarrow \mathbf{R}$ be integrable with

$$
\alpha(t) \leq \beta + L \int_{t_0}^t \alpha(s) ds
\label{eq02:lemma}
\tag{3}
$$

for some constant $\beta, L$ then

$$
\alpha(t) \leq \beta e^{L(t-t_0)}
$$

#### proof of Simple Version
Define $w(t) = \int_{t_0}^t \alpha(s) ds$. Then, since $w'(t) = \alpha(t)$, by $\eqref{eq02:lemma}$, we obtain

$$
\alpha(t) = w'(t) \leq \beta + L w(t)
$$

**It is important to solve a ordinary differential equation that let $w(t)$ be as follows with $f(t_0) = 0$**
$$
w(t) \leq e^{L(t - t_0)} f(t).
\label{eq03:Lemma}
\tag{4}
$$

$$
w'(t) \leq L \cdot e^{L(t - t_0)} f(t) + e^{L(t - t_0)} f'(t)
\label{eq04:Lemma}
\tag{5}
$$

In $\eqref{eq04:Lemma}$,since the first term is same to $L w(t)$ and the second term shall be $\beta$,  we regrad $f'(t)$ as follows:

$$
\begin{aligned}
f'(t)e^{L(t - t_0)} &= \beta \\
f'(t) &= \beta \cdot e^{-L(t-t_0)}
\end{aligned}
\label{eq05:lemma}
\tag{6}
$$

The Integration of the $\eqref{eq05:lemma}$ is

$$
f(t) - f(t_0) = \beta \int_{t_0}^t e^{-L(s - t_0)} ds 
\label{eq06:lemma}
\tag{7}
$$

Substitute $\eqref{eq06:lemma}$ to $\eqref{eq03:Lemma}$, we obtain

$$
\begin{aligned}
w(t) &\leq e^{L(t-t_0)}f(t_0) + e^{L(t-t_0)} \int_{t_0}^t e^{-L(s - t_0)}\cdot \beta ds \\
&\leq e^{L(t-t_0)}f(t_0) + \int_{t_0}^t  e^{L(t - s)}\cdot \beta ds
\end{aligned}
\label{eq07:lemma}
\tag{8}
$$

By assumption $f(t_0) = 0$, the $\eqref{eq07:lemma}$ is  

$$
w(t) \leq \int_{t_0}^t  e^{L(t - s)}\cdot \beta ds
\label{eq08:lemma}
\tag{9}
$$

Therefore, 

$$
w(t) = \int_{t_0}^t \alpha(s) ds \leq \int_{t_0}^t e^{L(t-s)} \beta ds \Rightarrow
\alpha (t) \leq \beta e^{L(t-t_0)}
$$

**Q.E.D**

#### proof of Grownwell's lemma
It is very similar to the proof of the sinple version. Suppose that all assumptions are hold, the $\eqref{eq06:lemma}$ is changed to

$$
f(t) = \int_{t_0}^t e^{-L(s - t_0)} \beta(s) ds, \;\;\because f(t_0) = 0
$$

Thereby, 

$$
w(t) \leq \int_{t_0}^t  e^{L(t - s)}\cdot \beta (s) ds
\label{eq09:lemma}
\tag{10}
$$

since $\alpha(t) = w'(t)$,  we  can obtain the following 

$$
\begin{aligned}
w'(t) = \alpha(t) 
&\leq \frac{\partial }{\partial t} \left( \int_{t_0}^t  e^{L(t - s)}\cdot \beta (s) ds \right) \\

&\leq \int_{t_0}^t  \frac{\partial }{\partial t} e^{L(t - s)}\cdot \beta (s) + e^{L(t - s)}\cdot \frac{\partial }{\partial t} \beta (s) \bigg\rvert_{t=s}ds \\

&\leq L \int_{t_0}^t e^{L(t - s)}\cdot \beta (s) ds + \int_{t_0}^t \frac{\partial }{\partial t} \beta (t) dt \\

&\leq L \int_{t_0}^t e^{L(t - s)}\cdot \beta (s) ds + \beta (t)
\end{aligned}
$$

**Q.E.D**
#### Note 
In final integration, correctly 

$$
\int_{t_0}^t \frac{\partial }{\partial t} \beta (t) dt = \beta(t) - \beta(t_0)
$$

However, since $\alpha(t) > 0, \; \forall t \in [t_0, T] $ , $\beta(t) > 0, \; \forall t \in [t_0, T] $. Therefore, it is possible to neglect the $\beta(t_0)$ term.

### Triple Squared Inequality
In stochastic Analysis, generally there are 3 terms in a target stochastic differential equation.
The first 2 terms are the first order and second order differential with respect to $t$ and the third term is the first order differential to Wiener process.

$$
(a + b + c)^2 \leq 3(a^2 + b^2 + c^2)
$$

### Cauchy Formula

$$
\int_{t_0}^t \int_{t_0}^{t_{n-1}} \cdots \int_{t_0}^{t_1} f(s) ds dt_1 \cdots dt_{n-1} = \frac{1}{(n-1)!} \int_{t_0}^t (t -s)^{n-1} f(s) ds
$$

이 공식은 다음과 같이 Stochastic Differential 혹은 Difference의 Analysis에서 

$$
\mathbb{E} \left( \| X_t^{(n+1)} - X_t^{(n)} \|^2 \right) \leq L \int_{t_0}^t \mathbb{E} \left( \| X_s^{(n+1)} - X_s^{(n)} \|^2 \right) ds
\label{eq09:CF}
\tag{11}
$$

방정식 $\eqref{eq09:CF}$를 다음과 같이 변환하기 위하여 사용한다.

$$
\mathbb{E} \left( \| X_t^{(n+1)} - X_t^{(n)} \|^2 \right) \leq \frac{L^n}{(n-1)!} \int_{t_0}^t (t -s)^{n-1} \mathbb{E} \left( \| X_s^{(1)} - X_s^{(0)} \|^2 \right) ds
$$

이는 **Discrete index (n)** 에 대한 **Continuous index t** 가 존재하는 경우에 대한 해석학적 표현에서 매우 중요한 방법론이다.


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
