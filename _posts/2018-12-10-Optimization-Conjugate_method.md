---
layout: post
title:  "[Lecture Note 9] Conjugate Method"
date:   2018-12-10 19:40:00 +0900
categories: [Mathematics, Optimization]
tags:
  - Nonlinear Optimization
  - UST Lecture
comments: true
---

* Table of Contents
{:toc}

## Quadratic Problem
$$
\min f(x) : f(x) = \frac{1}{2} \langle x, Qx \rangle - b^T x \;\;\;\;\;\text{ minimizer } x^* = Q^{-1}b \\
\nabla f(x) = Qx -b = g(x)
$$

### Steepest Descent
$$
x_{i+1} = x_i - \alpha_i g_i \;\;\;\;\; \alpha_i = \underset{\lambda \geq 0}{\arg}  \min f(x_i - \lambda g_i) 
$$

식(1)에서 최적 $\lambda$ 는 $\frac{\partial f}{\partial \lambda} = 0$을 만족한다. 즉, ($x = x_{i+1}$ 이라 생각하면, 그리고 $\alpha$ 대신 $\lambda$로 놓고 생각하면)
$$
\frac{\partial f}{\partial \lambda} = {\frac{\partial f}{\partial x}}^T \frac{\partial x}{\partial \lambda} = [Q(x_i - \lambda g_i) -b]^T(-g_i) = 0
$$
그러므로
$$
\begin{align}
0 &= [Q(x_i - \lambda g_i) -b]^T g_i = x_i^T Q g_i - \lambda g_i^T Q g_i -b^T g_i = (Q x_i - b)^T g_i - \lambda g_i^T Q g_i \\
&\implies (Q x_i - b)^T g_i = g_i^T g_i = \lambda g_i^T Q g_i \\
&\implies \lambda = \frac{g_i^T g_i}{g_i^T Q g_i}
\end{align}
$$
따라서,
$$
x_{i+1} = x_i - \frac{g_i^T g_i}{g_i^T Q g_i} g_i
$$

### Usage 
for any $f(x)$ and given $x_i$ $\rightarrow$ Second order approximation near $x_i$
$$
f(x) \approx f(x_i) + \langle \nabla f(x_i), x- x_i \rangle + \frac{1}{2} \langle x - x_i, Q(x- x_i) \rangle
$$

이러면 문제 
$$
\left. \min f(x) \right|_{x^*}, \;\;\; f(x) = \frac{1}{2} \langle x, Qx \rangle - b^T x
$$
에 대하여  Let
$$
F(x) = \frac{1}{2} \langle x - x^*, Q(x - x^*) \rangle
$$

#### Claim  
$\min f(x)$ and $min F(x)$ construct a same $\{x_i\}$ sequence.
#### proof of claim
$$
\begin{align}
F(x) &= \frac{1}{2} \langle x, Qx \rangle - {x^*}^T Q x + \frac{1}{2} \langle x^*, Qx^* \rangle &\\
&= \frac{1}{2} \langle x, Qx \rangle - b^T x + \frac{1}{2} \langle x^*, Qx^* \rangle  &\because \nabla f(x^*) = Qx^* - b = 0 \\
&= f(x) + \frac{1}{2} \langle x^*, Qx^* \rangle
\end{align}
$$
따라서 $\frac{\partial f}{\partial x} = \frac{\partial F}{\partial x}$ 그러므로 같은 최적화 문제가 된다. 

### Lemma
$$
F(x_{i+1}) = \left[ I - \frac{(g_i^T g_i)^2}{(g_i Q g_i)(g_i Q^{-1} g_i)}  \right] F(x_i)
$$
#### proof of Lemma
$$
g_i \triangleq Qx_i -b = Qx_i - Qx^{*} = Q(x_i - x^{*}) = Qy_i
$$
따라서, $F(x_i) = \frac{1}{2}y_i^T Q y_i$. 고로
$$
F(x_i) - F(x_{i+1}) = \frac{1}{2} [y_i Q y_i - y_{i+1} Q y_{i+1}]
$$
로 놓을 수 있으므로
$$
\begin{align}
y_{i+1}^T Q y_{i+1} &= (x_{i+1} - x^*)^T Q (x_{i+1} - x^*) = (x_i - \alpha_i g_i - x^*)^T Q (x_i - \alpha_i g_i - x^*) \\
&= (y_i - \alpha_i g_i)^T Q (y_i - \alpha_i g_i) \\
&= y_i^T Qy_i - 2 \alpha_i g_i^T Q y_i + \alpha_i^2 g_i^T Q g_i 
\end{align}
$$

따라서, Since $ \alpha = \lambda = \frac{g_i^T g_i}{g_i^T Q g_i} $
$$
\begin{align}
\frac{F(x_i) - F(x_{i+1})}{F(x_i)} &= - \frac{- 2 \alpha_i g_i^T Q y_i + \alpha_i^2 g_i^T Q g_i }{y_i^T Q y_i} = \frac{ 2 \alpha_i g_i^T Q Q^{-1} g_i - \alpha_i^2 g_i^T Q g_i}{g_i^T Q^{-1} Q Q^{-1} g_i} \\
&= \frac{ 2 \alpha_i g_i^T g_i - \alpha_i^2 g_i^T Q g_i}{g_i^T Q^{-1} g_i} = \frac{2 \frac{g_i^T g_i}{g_i^T Q g_i} g_i^T g_i - \frac{(g_i^T g_i)^2}{(g_i^T Q g_i)^2} g_i^T Q g_i}{g_i^T Q^{-1} g_i} \\
&= \frac{\frac{1}{g_i^T Q g_i}\left( 2(g_i^T g_i)^2 - (g_i^T g_i)^2 \right)}{g_i^T Q^{-1} g_i} \\
&= \frac{(g_i^T g_i)^2}{(g_i^T Q g_i)(g_i^T Q^{-1} g_i)}
\end{align}
$$

##  Method of Conjugate direction
### Definition 
A basis $\{u_i\}_{i=0}^{\infty}$ of $\mathbb{R}^n$ is said to be **orthogonal** if $\langle u_i, u_j \rangle = 0, \;\forall i \neq j$.

### Definition : Q- Conjugate
Given a symmetric positive definite matrix $Q$, a basis  $\{u_i\}_{i=0}^{\infty}$  is said to be **"Q- Conjugate"** if $\langle u_i, Qu_j \rangle = 0, \;\forall i \neq j$

### Theorem 
Let $f:\mathbb{R}^n \rightarrow \mathbb{R}$ be continously differentiable. Suppose that $\hat{x}$ minimizes $f(\cdot)$ on the subspace spanned by $\{y_1, \cdots y_n\}, k \leq n$, then  $\langle \nabla f(\hat{x}), y_i \rangle = 0, \; i=1, \cdots k$.

#### proof
Let $S$ be the subspace spanned by $\{y_1, \cdots y_n\}$ then the $S = \{y \in \mathbb{R}^n \}$ 
Since $\hat{x}$ is a minimizer on $S$ ($\min_{x \in S} f(x) = f(\hat{x})$)
$$
\exists \hat{\alpha} \in \mathbb{R}^n \;\;\text{ such that } \hat{x} = Y\ \hat{\alpha} \;\;\text{ where }\;\; Y = [y_1, \cdots y_k], \hat{\alpha} = [\hat{\alpha}_1, \cdots, \hat{\alpha}_k]^T
$$
Since any $x \in S$ can be represented $\alpha$ by $x = Y \alpha$ for some $\alpha \in \mathbb{R}^k$. Then
$$
\min_{x \in S} f(x) = \min_{\alpha \in \mathbb{R}^k} f(Y \alpha) \triangleq  \min_{\alpha \in \mathbb{R}^k} g(\alpha) \;\;\;\text{ such that } \;\;\;\left. \frac{\partial g}{\partial \alpha} \right|_{\alpha = \hat{\alpha}} = 0
$$
then (since $\hat{x} = Y \hat{\alpha}$, $\left. \frac{\partial x}{\partial \alpha} \right|_{x = \hat{x}, \alpha = \hat{\alpha}}= Y$)
$$
\frac{\partial g}{\partial \alpha} = \left( \frac{\partial f}{\partial x} \frac{\partial x}{\partial \alpha}\right)^T = \left( \nabla f(\hat{x})^T Y  \right)^T = Y^T \cdot \nabla f(\hat{x}) = 0
$$
Thus, 
$$
\langle \nabla f(\hat{x}), y_i \rangle = 0, \;\;\; \forall i = 1, \cdots k
$$

### Theorem 2
Let $H$ be a symmetric positive definite $n \times n$ matrix, and let $d \in \mathbb{R}^n$ be arbitrary.
Let $ f(x) = \frac{1}{2} \langle x, Hx \rangle + \langle d, x \rangle $
Let $\{ h_i \}_{i=0}^{n-1} $ be on H-conjugate basis for $\mathbb{R}^n$
If $\{ x_i \}_{i=0}^h$ is a sequence constructed according to $x_0$ given by
$$
\begin{align}
x_{i+1} &= x_i - \lambda_i h_i \\
\lambda_i &= \arg \min_{\lambda \geq 0} f(x_i - \lambda h_i)
\end{align}
$$
then $x_i$ minimizes $f(\cdot)$ on the subspace spanned by $h_0, \cdots , h_{i-1}$
(즉, $\mathbb{R}^1$ span하여 최소, $\rightarrow$ $\mathbb{R}^2$ span하여 최소 .... $\mathbb{R}^n$ span하여 최소로 가져가는 것)

#### proof
Since $f$ is strictly convex
$\hat{x}$ is a minimizer of $f(\cdot)$ on the subspace spanned by 
$$
\{y_i, \cdots, y_k \} \Leftrightarrow \langle \nabla f(\hat{x}), y_i \rangle = 0 \;\;\;\; i=1, \cdots k
$$
- 이는 앞에서 증명한 바 당연하다.

It is necessary to prove that $\langle \nabla f(x_i), h_j \rangle = 0$, for $j=0, \cdots i-1$
먼저 $\nabla f(x_i)$는
$$
\nabla f(x_i) = Hx_i + d_i = g_i 
$$
다음 $\lambda_i$는 가정에서 $f(x_i -\lambda h_i)$를 최소화 시켜야 하므로
$$
0 = \left. \frac{\partial f}{\partial \lambda} \right|_{\lambda=\lambda_i} = {\frac{\partial f}{\partial x}}^T \cdot {\left. \frac{\partial x}{\partial \lambda} \right|_{\lambda = \lambda_i}} = \nabla f(x_i - \lambda_i h_i)^T (-h_i)
$$
그러므로
$$
\langle g_{i+1}, h_i \rangle = 0, \;\;\; \forall i=0, \cdots , n-1
\tag{1}
$$
Thus
$$
\begin{align}
g_i &= H x_i + d \\
&= H(x_{i-1} - \lambda_i h_{i-1}) + d \\
&= g_{i-1} - \lambda_{i-1} H h_{i-1} \\
&= - \lambda_{i-1} H h_{i-1} - - \lambda_{i-2} H h_{i-2} - \cdots - - \lambda_{0} H h_{0} + g_0
\end{align}
$$

Since $\{ h_i \}$ are H-conjugate (It means that $\langle h_i, Hh_i \rangle = 0, \;\; j \neq i$ )
$$
\begin{align}
\langle g_i, h_i \rangle &= -\lambda_{i-1} \langle H h_{i-1}, h_i \rangle -\lambda_{i-2} \langle H h_{i-2}, h_i \rangle - \lambda_{0} \langle H h_{0}, h_i \rangle + \langle g_0, h_i \rangle \\
&= \langle g_0, h_i \rangle
\end{align}
\tag{2}
$$
그리고 for $k < i$ 에 대해서는 방정식 (2)에서 0이 되지 않는 항 $- \lambda _k \langle h_k, Hh_k \rangle $ 이 하나 존재하므로
$$
\langle g_i, h_k \rangle = \langle g_0, h_k \rangle - \lambda _k \langle h_k, Hh_k \rangle 
$$
Let $i=k+1$ 즉, $k=i-1$ then 식 (1)에서 
$$
0 = \langle g_{k+1}, h_k \rangle = \langle g_0, h_k \rangle - \lambda _k \langle h_k, Hh_k \rangle
$$

따라서 임의의 $\bar{k} < k < i $ 에 대하여   
$$
\langle g_{i}, h_{\bar{k}} \rangle = \langle g_0, h_{\bar{k}} \rangle - \lambda_{\bar{k}} \langle h_{\bar{k}}, Hh_{\bar{k}} \rangle = 0
$$
그러므로
$$
\langle g_i, h_k \rangle = \langle \nabla f(x_i), h_k \rangle = 0 \;\;\;\;\; \text{for } k=1, \cdots i-1
$$
**Q.E.D **

## Conjugate Method
$$
\text{solve   }\;\;\;\; \min_{x \in \mathbb{R}^n} \frac{1}{2} \langle x, Hx \rangle + \langle d, x \rangle, \;\;\; H > 0
$$

| Procesdure | Processing|
|---|---|
| Data | $x_o \in \mathbb{R}^n$ |
| Step 0 | Set $i=0$, $h_0 = g_0 = Hx_0 + d$ |
| Step 1 | Compute the step length |
|        | $ \lambda_i = \arg \min f(x_i - \lambda_i h_i)$ |
| Step 2 | update, Set |
|        | $x_{i+1} = x_i - \lambda_i h_i$ |
|        | $g_{i+1} = Hx_{i+1} + d$ |
|        | $ h_{i+1} = g_{i+1} + h_i r_i$ |
|        | so that $\langle h_{i+1}, Hh_i \rangle = 0$ |
| Step 3 | Replace $i $ by $i+1$ and goto Step 1 |

where $r_i$ is defined as
$$
r_i = -\frac{\langle Hh_i, g_{i+1} \rangle }{\langle h_i , Hh_i \rangle}
$$

### Theorem 1
Suppose that $H$ is an $n \times n$ **positive semi-definite symmetric matrix** and $d \in \mathbb{R}^n$ arbitrary, then the conjugate gradient method solves the problem 
$$
\min_{x \in \mathbb{R}^n} \frac{1}{2} \langle x, Hx \rangle + \langle d, x \rangle
$$
in **at most $n$ iterations **

#### proof
이 증명은 조금 문제가 있으므로 추가 검토가 필요하다.

- We need to prove that $\langle h_i Hh_j \rangle = 0$ for $i \neq j$
By induction, since $h_0 = g_0$
$$
\begin{align}
\langle g_1, h_0 \rangle &= \langle Hx_1 + d, h_0 \rangle \\ 
&= \langle H(x_0 - \lambda_0 h_0) + d, h_0 \rangle\\
&=\langle Hx_0 + d - \lambda H h_0, h_0 \rangle 
\end{align}
\tag{3}
$$
at $\lambda = \lambda_0$
$$
\begin{align}
\left. \frac{\partial f}{\partial \lambda} \right|_{\lambda = \lambda_0} &= \left. {\frac{\partial f}{\partial x}}^T \frac{\partial x}{\partial \lambda} \right|_{\lambda = \lambda_0} = \langle {\left. Hx + d \right|_{x = x_0 - \lambda_0 h_0 }}, -h_0 \rangle  \\
&= \langle Hx_0 - \lambda_0 H h_0 + d, -h_0 \rangle = 0
\end{align}
$$
이므로 식(3)은
$$
\langle Hx_0 + d - \lambda H h_0, h_0 \rangle = 0
\tag{4}
$$
$\langle h_{i+1}, Hh_i \rangle = 0$ 조건에서 $\langle h_{1}, Hh_0 \rangle = 0$ 이고 이 조건을 만족하기 위한 $r_i$를 구하면
$$
0 = \langle Hh_i, h_{i+1} \rangle = \langle Hh_i, g_{i+1} + r_i h_i \rangle = \langle  Hh_i, g_{i+1} \rangle + r_i \langle Hh_i, h_i \rangle = 0
$$
따라서
$$
r_i = - \frac{\langle  Hh_i, g_{i+1} \rangle}{\langle Hh_i, h_i \rangle}
$$

- 먼저, 다음의 가정을 놓는다. 

$i=k$, Suppose that $\langle g_i, g_j \rangle = 0$ and $\langle h_i, Hh_j \rangle = 0$ for $ 0 \leq i, j \leq k < n$ with $i \neq j$

let $i = k+1$ need to prove that
$$
\langle g_{k+1}, g_i \rangle = 0, \langle h_{k+1}, H h_i \rangle = 0 \;\;\;\; \text { for } i=0, \cdots, k 
$$

식 (4)에서 0 대신 $i$를 대입하면 
$$
\langle g_{k+1}, h_i \rangle = 0
$$
이는 다시말해 $g_{k+1} = Hx_{i+1} + d = H(x_i -\lambda_i h_i) + d$ 에서
$$
\langle Hx_i + d - \lambda_i H h_i, h_i \rangle = 0 \Leftrightarrow \langle g_i, h_i \rangle - \lambda_i \langle Hh_i, h_i \rangle = 0
$$
따라서
$$
\lambda_i = \frac{\langle g_i, h_i \rangle}{\langle Hh_i, h_i \rangle}
$$

이 결과를 사용하여 본격적으로 $\langle g_{k+1}, g_i \rangle = 0$ 를 증명한다.

$$
\begin{align}
\langle g_i, g_{i+1} \rangle &= \langle g_i, g_i - \lambda_i H h_i \rangle \\
&= \langle g_i, g_i \rangle - \lambda_i \langle g_i, Hh_i \rangle 
&= \langle g_i, g_i \rangle - \frac{\langle g_i, h_i \rangle \cdot \langle g_i, Hh_i \rangle}{\langle  h_i, Hh_i \rangle}
\end{align}
\tag{5}
$$
(식 (5)의 마지막 항은 매우 중요하다.)
$$
\begin{align}
\langle g_i, h_i \rangle &= \langle g_i, g_i + r_{i-1} h_{i-1} \rangle &\\
&= \langle g_i, g_i \rangle + r_{i-1} \langle g_i, h_{i-1} \rangle &\\
&= \langle g_i, g_i \rangle &\because  \langle g_i, h_{i-1} \rangle = 0
\end{align}
$$
and
$$
\begin{align}
\langle h_i, Hh_i \rangle &= \langle g_i + r_{i-1}h_{i-1}, Hh_i \rangle &\\
&= \langle g_i, Hh_i \rangle + r_{i-1} \langle h_{i-1}, Hh_i \rangle & \\
&= \langle g_i, Hh_i \rangle  &\because \langle h_{i-1}, Hh_i \rangle  = \langle h_i, Hh_{i-1} \rangle = 0 (\text { by Symmetric of } H) 
\end{align}
$$
그러므로
$$
\langle g_i, g_{i+1} \rangle = \langle g_i, g_i \rangle - \frac{\langle g_i, h_i \rangle \cdot \langle g_i, Hh_i \rangle}{\langle  h_i, Hh_i \rangle} = 0
$$
따라서
$$
\forall i, \langle g_i, g_{i+1} \rangle = 0 \Rightarrow \text{ if } i=k, \langle g_k, g_{k+1} \rangle = 0
$$
여기까지 증명에서 index 1의 차이가 나는 vector들은 Orthogonal 함이 증명되었다.
그러나, 일반적인 경우 즉,  $i=1, \cdots k-1$ 과 $k$의 Orthogonal 함은 아직 증명되지 않았다. 따라서 이를 증명한다.

Let $i \neq 0, \; i < k$ i.e. $ i=1, \cdots k-1$,
$$
\langle g_{k+1}, g_i \rangle = \langle g_k - \lambda_k H h_k, g_i \rangle = \langle g_k, g_i \rangle - \lambda_k \langle H h_k, g_i \rangle
$$
가정 $\langle g_i, g_j \rangle = 0$ for $ 0 \leq i, j \leq k < n$ with $i \neq j$ 에서
- 위 가정 보다는 만일 $i = k-1$ 이면 위 식은 Index 1 차이가 나므로 $\langle g_k, g_i \rangle = 0$, 이것을 확대 시켜나가는 방식으로 증명하는 것이 더 낫다.

$$
\langle g_k, g_i \rangle = 0 
$$
이므로 위 식은 
$$
\langle g_{k+1}, g_i \rangle = - \lambda_k \langle H h_k, h_i - r_{i-1}h_{i-1} \rangle = - \lambda_k \langle H h_k, h_i \rangle + \lambda_k r_{i-1} \langle H h_k, h_{i-1} \rangle
$$
여기에서 가정 $\langle h_i, Hh_j \rangle = 0$ for $ 0 \leq i, j \leq k < n$ with $i \neq j$ 에 의해
$$
\langle H h_k, h_i \rangle  = 0, \;\;\;\; \langle H h_k, h_{i-1} \rangle = 0  \tag{6}
$$
따라서 
$$
\langle g_{k+1}, g_i \rangle = 0
$$

마지막으로 $i=0$에 대하ㅣ여 살펴보면
$$
\begin{align}
\langle g_{k+1}, g_0 \rangle &= \langle g_k - \lambda_k H h_k, g_0 \rangle & \\
&= \langle g_k, g_0 \rangle - \lambda_k \langle Hh_k, g_0 \rangle  & \because \langle g_k, g_0 \rangle = 0 \\
&= - \lambda_k \langle H h_k, h_0 \rangle & \because g_0 = h_0, \;\;\text{ and }\langle H h_k, h_0 \rangle = 0 \\
&= 0
\end{align}
$$
그러므로 $\{g_i \}$는 모두 Orthogonal, 즉, Orthogonal BAsis $g_i$를 찾은 것이다.

마지막으로, $\langle h_{k+1}, Hh_k \rangle = 0$ 이므로 (첫번째 증명에서)
for $i=0, \cdots k-1$
$$
\begin{align}
\langle h_{k+1}, Hh_i \rangle &= \langle g_{k+1} + r_k h_k, Hh_i \rangle &\\
&= \langle g_{k+1}, Hh_i \rangle + r_k \langle h_k, Hh_i \rangle  & \because \langle h_k, H h_i \rangle = 0 \text{ by (6)} \\
&= \langle H x_{i+1} + d, Hh_i \rangle &\because g_{i+1} = g_i - \lambda_i H h_i \\
&= \langle g_i - \lambda_i H h_i, H h_i \rangle &\because \frac{1}{\lambda_i}(g_{i+1} - g_i) = Hh_i \\
&= \langle g_{k+1},  \frac{1}{\lambda_i}(g_{i+1} - g_i) \rangle = 0
\end{align}
$$
따라서 $h$- conjugate가 증명
**Q.E.D **

## General Case
$\min_{\mathbb{R}^n} f(x)$에 대하여 다음의 아이디어를 적용한다.
Conjugate method에서 실제 Hessian을 구하는 것은 어려운 문제이다. 따라서 이를 Gradient로 Estimation 한다. 즉,
$$
r_i = -\frac{\langle Hh_i, g_{i+1} \rangle }{\langle h_i, Hh_i \rangle}
$$
등에서 $H$를 구하기 어렵다. 그러므로 
$$
g_{i+1} = g_i - \lambda_i H h_i \Leftrightarrow Hh_i = \frac{1}{\lambda}(g_i - g_{i+1})
$$
그러므로
$$
r_i = -\frac{\langle \frac{1}{\lambda}(g_i - g_{i+1}), g_{i+1} \rangle}{\langle h_i, \frac{1}{\lambda}(g_i - g_{i+1})  \rangle} = - \frac{\langle g_{i+1}, g_{i+1} \rangle - \langle g_i, g_{i+1} \rangle}{\langle h_i, g_i \rangle}
$$
Since $h_i = g_i + r_{i-1} h_{i-1}$ 
$$
\langle h_i, g_i \rangle = \langle g_i + r_{i-1} h_{i-1}, g_i \rangle = \langle g_i, g_i \rangle + r_{i-1} \langle h_{i-1}, g_i \rangle = \|g_i\|^2 + 0
$$
따라서
$$
r_i = - \frac{\langle g_{i+1}, g_{i+1} \rangle - \langle g_i, g_{i+1} \rangle}{\| g_i \|^2}
$$
따라서 다음의 두 가지 방법이 유도 된다.
- **Polak - Riebel Formula**

$$
r_i = - \frac{\langle g_{i+1}, g_{i+1} \rangle - \langle g_i, g_{i+1} \rangle}{\| g_i \|^2}
$$

- **Fletcher-Reeves Formula **
   - Since for the quadratic case, $\langle g_{i+1}, g_{i} \rangle = 0$, that results can be extended.
$$
r_i = - \frac{\| g_{i+1} \|^2}{\| g_i \|^2}
$$

## General Conjugate Gradient Algorithm

| Procesdure | Processing|
|---|---|
| Data | $x_o \in \mathbb{R}^n$ |
| Step 0 | Set $i=0$, $h_0 = \nabla f(x_0)$ |
| Step 1 | Compute the step length |
|        | $ \lambda_i = \arg \min f(x_i - \lambda_i h_i)$ |
| Step 2 | update, Set |
|        | $x_{i+1} = x_{i} - \lambda_i h_i$ |
|        | Set $r_i^{PR}$, $r_i^{FR}$  |
|        | $h_{i+1} = \nabla f(x_{i+1}) + r_i^{PR} h_i$ or $h_{i+1} = \nabla f(x_{i+1}) + r_i^{FR} h_i$ |
| Step 3 | Replace $i $ by $i+1$ and goto Step 1 |

where $r_i^{PR}$, $r_i^{FR}$ is defined as
$$
\begin{align}
r_i^{PR} &= -\frac{\langle \nabla f(x_{i+1}) - \nabla f(x_i), \nabla f(x_{i+1}) \rangle }{\| \nabla f(x_{i}) \|^2} \\
r_i^{FR} &= -\frac{\|\nabla f(x_{i+1}) \|^2 }{\| \nabla f(x_{i}) \|^2}
\end{align}
$$

### Theorem 1
Suppose that $f: \mathbb{R}^n \rightarrow \mathbb{R}$ is twice continuous differentiable and 
$$
\exists 0 < m \leq M \;\;\;  \text{   such that   } \;\;\; \forall x,y \in \mathbb{R}^n, \;\; m \|y\|^2 \leq \langle y, H(x)y \rangle \leq M \|y\|^2
$$
Polak-Riebler algorithm is applied to solve $\min f(x)$ producing a sequence $\{ x_i \}_{i=0}^{\infty}$ then
- $\exists \rho \in (0,1) \;\;\; \text{such that} \;\;\; \langle \nabla f(x_i), h_i \rangle \geq \rho \|\nabla f(x_i) \| \| h_i \|$
- The sequence $\{ x_i \}_{i=0}^{\infty}$ converges to $\hat{x}$, the unique minimizer of $f(\cdot)$.

(위의 것을 만족하면 아래 명제도 만족됨)

#### proof of 1.
let $ g_i = \nabla f(x_i) $, then
$$
\begin{align}
g_{i+1} &= \nabla f (x_{i+1}) = \nabla f( x_i - \nabla_i h_i) \\
&= \nabla f(x_i) + \int_0^1 H(x_i - s \lambda_i h_i )(-\lambda_i h_i) ds \\
&= g_i - \lambda_i \int_0^1 H(x_i - s \lambda_i h_i ) h_i ds
\end{align}
$$
Now, $\langle g_{i+1}, h_i \rangle = 0$ by construction (because of $h$- conjugate)
It means that $\langle g_{i} - \lambda_i H_i h_i, h_i \rangle = 0$. Thus,

$$
\begin{align}
\lambda_i &= \frac{\langle g_i, h_i \rangle}{\langle Hh_i, h_i} &\text{in algorithm} h_i = g_i + r_{i-1}^{PR} h_{i-1}
&= \frac{\langle g_i, g_i + r_{i-1}^{PR} h_{i-1} \rangle}{\langle Hh_{i-1}, h_i \rangle} = \frac{\|g_i\|^2}{\langle Hh_{i-1}, h_i \rangle}
\end{align}
$$

and

$$
r_{i}^{PR} = \frac{\langle g_{i+1} - g_i, g_{i+1}  \rangle}{\| g_i \|^2} = -\lambda_i \frac{\langle Hh_i, g_{i+1} \rangle}{\| g_i \|^2} = -\frac{\langle Hh_i, g_{i+1} \rangle}{\langle Hh_{i}, h_i \rangle}
$$

그러므로

$$
\| r_{i}^{PR} \| \leq \frac{M \| h_i \| \| g_{i+1} \|}{m \| h_i \|^2} = \frac{M}{m} \cdot \frac{\| g_{i+1} \|}{\| h_i \|}
$$
그리고
$$
\| h_{i+1} \| \leq \| g_{i+1} \| + \frac{M}{m} \frac{\| g_{i+1} \|}{\| h_i \|} \cdot \|h_i \| = (1 + \frac{M}{m}) \| g_i \|
$$

마지막으로, Since $\langle g_{i+1}, h_i \rangle = 0$
$$
\langle g_{i+1}, h_{i+1} \rangle = \langle g_{i+1}, g_{i+1} + r_i^{PR} h_i \rangle = \| g_{i+1} \|^2
$$

따라서
$$
\frac{\langle g_{i+1}, h_{i+1} \rangle}{\| g_{i+1} \| \| h_{i+1} \| } = \frac{\| g_{i+1} \|^2}{\| g_{i+1} \| \| h_{i+1} \|} \geq \frac{\| g_{i+1} \|^2}{(1+ \frac{M}{m}) \| g_{i+1} \|} = \frac{1}{1+ \frac{M}{m}} \triangleq \rho
$$
위에서 구한 $\rho$ 는 $0 < \rho < 1$ 이다. 따라서
$$
\langle g_{i+1}, h_{i+1} \rangle \geq \rho \| g_{i+1} \| \|h_{i+1} \| 
$$

**Q.E.D**

### Theorem 2
If Fletcher-Reeves algorithm is applied to solve $\min f(x)$ then 
(a) $\exists \{ t_i \}_{i=0}^{\infty}$ 
- $t_i > 0, \;\; \forall i$
- $t_i \rightarrow 0 \;\;\; \text{as} \;\;\; i \rightarrow \infty$
- $\sum_{i=0}^k t_i^2 \rightarrow \infty \;\;\; \text{as} \;\;\; k \rightarrow \infty$
- $\langle \nabla f(x_i), h_i \rangle \geq t_i \| \nabla f(x_i) \| \| h_i \|$

(b) $\{ x_i \}$ converges to $\hat{x}$, the unique minizer.

증명은 생략한다. 

### Note
- Quadratic Case에서 Step Size $\lambda_i$는 다음과 같이 계산된다.
$$
\lambda_i = \frac{\langle g_i, h_i \rangle}{\langle Hh_i, h_i \rangle}
$$

- Conjugate의 결과는 결국 이렇게 되는 것이다.
$$
\langle g_i, h_k \rangle = \langle \nabla f(x_i), h_k \rangle = 0 \;\;\;\;\; \text{for } k=1, \cdots i-1
$$

