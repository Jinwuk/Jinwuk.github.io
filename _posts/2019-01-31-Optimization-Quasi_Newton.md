---
layout: post
title:  "[Lecture Note 10] Quasi Newton"
date:   2018-12-10 19:40:00 +0900
categories: [Mathematics, Optimization]
tags:
  - Nonlinear Optimization
  - UST Lecture
comments: true
---

* Table of Contents
{:toc}

다음과 같은 Quadratic Problem을 생각해 보면
$$
\min_{x \in \mathbb{R}^n} f(x) \Rightarrow f(x) = \frac{1}{2} \langle x, Hx \rangle + \langle d, x \rangle
$$

#### Newton Method
$$
x_{i+1} = x_i - \lambda_i H^{-1} g_i \;\;\; \text{where }\;\; g_i = \nabla f(x_i) = Hx + d
$$
- We need only 1 iteration to find the minimizer
- However, the problem finding $H$ is so expensive

#### Steepest Descent
$$
x_{i+1} = x_i - \lambda_i g_i \;\;\; \text{where }\;\; g_i = \nabla f(x_i), \;\; \lambda_i = \arg \min f(x_i - \lambda g_i)
$$

#### Conjugate Method
$$
x_{i+1} = x_i - \lambda_i h_i \;\;\; \text{update } h_i \text{ so that } h_i \text{ is } H \text{-Conjugate}
$$
- It needs at most $n$ iterations to find the minimizer

#### Quasi Newton
Estimate the Hessian $H$ i.e. construct a sequence of $\{ H_i \}$ so that $H_i \rightarrow H $ 
(or construct a sequence of $\{ \beta_i \}$ so that $ \beta_i \rightarrow \beta = H^{-1}$ )
Update rule
$$
x_{i+1} = x_i - \lambda_i \beta_i g_i
$$

- 위와 같은 Quadaratic Problem의 경우 최대 $n$ iterations 이 minimizer를 찾는데 필요. (i.e. $\beta_n = H^{-1}$)

## Quasi Newton : Variable metric method
### Idea
$\min_{x \in \mathbb{R}^n} f(x)$ 를 2차 함수 근사화 하는 것 즉, 다음과 같이 근사하여 생각한다.
$$
f(x) = \langle d, x \rangle + \frac{1}{2} \langle x , Hx \rangle 
$$
given a positive definite $n \times n$ Matrix $H$.

이때, 다음과 같이 Search Direction을 놓는다고 가정하자. (아래의 경우 $df(x, h)$ 에서 $df(x, h) = 0$ 이 되면 최적이다.)
그리고, 다음 조건을 통해 Search Direction의 특성을 분석한다.

Search direction : $h(x) = \arg \min \{ \frac{1}{2} \| h \|_H^2 + df(x, h) \}$

#### Steepest descent의 경우
$$
h(x) = \arg \min \{ \frac{1}{2} \| h \|^2 + \langle \nabla f(x), h \rangle \}, \;\;\; \frac{\partial h(x)}{\partial h} = h + \nabla f(x) = 0 \Rightarrow h(x) = - \nabla f(x)
$$

#### Newton Method의 경우
$$
h(x) = \arg \min \{ \frac{1}{2} \| h \|_H^2 + df(x, h) \}
$$
where $H$ is the Hessian of $f(x)$ at $x$

$$
\frac{\partial h(x)}{\partial h} = Hh + \nabla f(x) = 0 \Rightarrow h = -H^{-1} \nabla f(x)
$$

#### Quasi Newton의 아이디어
Hessian $H$ 대신 $Q$ Matrix를 통해
$$
h(x) = \arg \min \{ \frac{1}{2} \| h \|_Q^2 + df(x, h) \}
$$

Newton 방법을 살펴보면
Let $f(x) = \langle d, x \rangle + \frac{1}{2} \langle x , Hx \rangle$. Let $x_0, \cdots x_n$ be a sequence of distict vectors, and let $B = H^{-1}$ 
Set
$$
\begin{align}
g_i &= \nabla f(x_i) = Hx + d, \\
\Delta x_i &= x_{i+1} - x_i, \\
\Delta g_i &= g_{i+1} - g_i = Hx_{i+1} + d - Hx_i - d = H\Delta x_i \\
& \Rightarrow H^{-1}\Delta g_i = \Delta x_i \;\;\; \text{or} \;\;\; B \Delta g_i = \Delta x_i \;\; \forall i \\
& \Rightarrow B [\Delta g_0 \cdots \Delta g_{n-1}] = [\Delta x_0 \cdots \Delta x_{n-1}] \\
& \Rightarrow B \Delta G = \Delta X
\end{align}
$$

만일, $\Delta G$ is non-singular, then 
$$
B = H^{-1} = \Delta X \Delta G^{-1}
$$

One starts with $B_0$, a Symmetric Positive Definite $n \times n$ which is an **initial guess of $H^{-1}$** and $x_0$ .
그리고 다음의 update rule을 생각해 본다면
$$
x_{i+1} = x_i - \lambda_i \beta_i g_i
$$
여기서 $\lambda_i$는 다음으로 정의된다.
$$
\lambda_i = \arg \min f(x_i - \lambda_i \beta_i g_i)
$$
여기서 $\beta_{i+1}$은 반드시 다음의 Quasi-Newton 특성을 만족하여야 한다.
$$
\beta_{i+1} \Delta g_k = \Delta x_k, \;\;\; k=0, 1, \cdots, i
$$

**Example **
$$
\beta_0 = I = 
\begin{bmatrix}
1  & 0  & 0 \\
0  & 1  & 0 \\
0  & 0  & 1
\end{bmatrix}
, \;\;\; 
\Delta g_0 = 
\begin{bmatrix}
2 \\
0 \\
0
\end{bmatrix}
, \;\;\; 
\Delta x_0 = 
\begin{bmatrix}
1 \\
1 \\
1
\end{bmatrix}
$$
여기서 Quasi Newton 조건을 만족하는 $\Delta \beta$를 찾는 문제
$$
\beta_1 = \beta_0 + \Delta \beta \;\;\;\text{ so that }\;\;\; 
\beta_1 \cdot 
\begin{bmatrix}
2 \\
0 \\
0
\end{bmatrix}
= 
\begin{bmatrix}
1 \\
1 \\
1
\end{bmatrix}
$$
간단히 
$$
\beta_1 =
\begin{bmatrix}
\frac{1}{2}  & 0  & 0 \\
\frac{1}{2}  & 1  & 0 \\
\frac{1}{2}  & 0  & 1
\end{bmatrix}
\;\;\;
\Delta \beta = 
\beta_1 - \beta_0=
\begin{bmatrix}
-\frac{1}{2}  & 0  & 0 \\
\frac{1}{2}  & 0  & 0 \\
\frac{1}{2}  & 0  & 0
\end{bmatrix}
$$
그러므로
$$
x_2 = x_1 - \lambda_1 \beta_1 g_i, \;\;\; g_2 = \nabla f(x_2)
$$
여기서
$$
\Delta g_1 = g_2 - g_1 =
\begin{bmatrix}
0 \\
1 \\
1
\end{bmatrix}
,\;\;\;
\Delta x_1 = x_2 - x_1 =
\begin{bmatrix}
2 \\
3 \\
1
\end{bmatrix}
$$
이라 하면
$\beta_2 = \beta_1 + \Delta \beta_1$ find $\Delta \beta_1$ so that $\beta_2 \Delta g_i = \Delta x_i$ for $i=0,1$ 

다시 말하면
$$
\beta_2 \Delta g_0 = \Delta x_0 \Rightarrow (\beta_1 + \Delta \beta_1) \Delta g_0 = \Delta x_0 \Rightarrow \Delta \beta_1 \Delta g_0 = 0 \\
\therefore \Delta g_0 \in \mathcal{N}(\Delta \beta_1)
$$
또한
$$
\beta_2 \Delta g_1 = \Delta x_1 \Rightarrow (\beta_1 + \Delta \beta_1) \Delta g_1 = \Delta x_1 \Rightarrow \beta_1 \Delta g_1 - \Delta x_1 = -\Delta \beta_1 \Delta g_1 \\
\therefore \Delta g_1 \in \mathcal{R}(\Delta \beta_1)
$$

## Generating $\beta_j$
**Quasi Newton Property**
$$
\beta_{i+1} \Delta g_k = \Delta x_k, \;\;\; k=0,1, \cdots i
$$

### Proposition : Rank-One Method
Supppose that $H$ is an $n \times n$ nonsingular matrix and 
let $\beta = H^{-1}$
let $H^* = H + ab^T$ for some $a, b \in \mathbb{R}^n$
If $\beta^* = {H^*}^{-1}$ exists, then it is given by
$$
\beta^* = \beta - \frac{\beta ab^T \beta}{1 + b^T \beta a}
$$

**Note : $ab^T$ 의 성질**

- $ab^T$ 의 Range space : $a$ 에 의해 Span 된다 $b^T x$ 는 Scalar 이므로 즉

$$
ab^T x = a(b^T x)
$$

- $ab^T$ 의 Null space : $b$가 $x$의 Orthogonal Space 

$$
a(b^T x) = 0
$$

#### proof
Since $\beta^*$ exists
we can set $\beta^* = \beta + \Delta \beta$, then

$$
\begin{align}
\beta^* H^* = I &= (\beta + \Delta \beta)(H + ab^T) = \beta H + \beta ab^T + \Delta \beta ab^T + \Delta \beta H \\
&= I + \beta ab^T + \Delta \beta H^*
\end{align}
$$
그러므로 다음이 성립해야 한다.
$$
0 = \beta ab^T + \Delta \beta H^* \tag{1}
$$
그리고
$$
\Delta \beta H^* = -\beta ab^T \Rightarrow \Delta \beta = -\beta ab^T {H^*}^{-1} \triangleq \beta a C^T \therefore C^T \triangleq b^T {H^*}^{-1} \in \mathbb{R}^n  \tag{2}
$$
Substitute (2) into (1)
$$
\begin{align}
0 &= \beta ab^T + \beta aC^T H^* = \beta a (b^T + C^T H + C^T ab^T) \Rightarrow b^T + C^T H + C^T ab^T = 0 \\
C^T H &= -(1 + C^T a)b^T \Rightarrow C^T = -(1+C^T a)b^T H^{-1} = -(1+C^T a)b^T \beta \tag{3}
\end{align}
$$

식 (3)을 다시 정리하면
$$
C^T = -(1+C^T a)b^T \beta \Rightarrow C^T = -b^T \beta - C^T ab^T \beta
$$
여기에 $a$를 곱하면
$$
C^T a = -b^T \beta a- C^T ab^T \beta a \in \mathbb{R} \Rightarrow C^T a (1 + b^T \beta a) = -b^T \beta a
$$
그러므로 
$$
C^T a = \frac{-b^T \beta a}{1+ b^T \beta a}  \tag{4}
$$
Substitute (4) into (3)
$$
\begin{align}
C^T = -b^T \beta + \frac{b^T \beta a b^T \beta}{1+ b^T \beta a} &= \frac{-b^T\beta(1+b^T \beta a) + b^T \beta a b^T \beta}{1 + b^T \beta a} \\
&= \frac{-b^T\beta -b^T\beta a b^T \beta  + b^T \beta a b^T \beta}{1 + b^T \beta a} \\
&= \frac{-b^T \beta}{1 + b^T \beta a}
\end{align}
$$
따라서
$$
\beta^* = \beta + \Delta \beta = \beta + \beta aC^T = \beta - \frac{\beta ab^T \beta }{1 + b^T \beta a}
$$
**Q.E.D**

### Compute $\beta_{i+1}$
Let $\beta_0 = I$ using a update value $\beta_{i+1} = \beta_i + \alpha_i z_i z_i^T$ (이것을 **rank-1 Property** 라고 한다)for $i=0, 1, 2, \cdots$ with $\beta_{i+1}$ required to satisfy. $\beta_{i+1} \Delta g_k = \Delta x_k$, $k=0, 1, \cdots, i$
where $x_i, \Delta x_i, \Delta g_i$ are computed by
$$
\begin{align}
x_{i+1} &= x_i - \lambda_i \beta_i g_i \\
\lambda_i &= \arg \min f(x_i - \lambda \beta_i g_i) \\
g_i &= \nabla f(x_i) \\
\Delta x_i &= x_{i+1} - x_i \\
\Delta g_i &= g_{i+1} - g_i
\end{align}
$$

### Find $\alpha_i, z_i$
Quasi-newton property has to be satisfied. i.e. $\beta_{i+1} \Delta g_i = \Delta x_i$
$$
\begin{align}
(\beta_i + \alpha_i z_i z_i^T) \Delta g_i = \Delta x_i  &\Rightarrow \Delta x_i = \beta_i \Delta g_i + \alpha_i z_i \langle z_i, \Delta g_i \rangle \\
&\Rightarrow \alpha_i z_i = \frac{\Delta x_i - \beta_i \Delta g_i}{\langle z_i, \Delta g_i \rangle}
\end{align}
\tag{5}
$$
Since
$$
\begin{align}
\langle \Delta x_i, \Delta g_i \rangle &= \langle \Delta g_i, \beta \Delta g_i \rangle + \alpha_i \langle z_i, \Delta g_i \rangle^2 \\
\alpha_i \langle z_i, \Delta g_i \rangle^2 &= -\langle \Delta g_i, \beta_i \Delta g_i - \Delta x_i \rangle = \langle \Delta g_i, \Delta x_i - \beta_i \Delta g_i \rangle 
\end{align}
\tag{6}
$$
Substitute (5), (6) into $\beta_{i+1} = \beta_i + \alpha_i z_i z_i^T$ 
$$
\begin{align}
\beta_{i+1} &= \beta_i + \frac{\Delta x_i - \beta_i \Delta g_i}{\langle z_i, \Delta g_i \rangle} \left( \frac{\Delta x_i - \beta_i \Delta g_i}{\alpha \langle z_i, \Delta g_i \rangle} \right)^T \\
&= \frac{(\Delta x_i - \beta_i \Delta g_i)(\Delta x_i - \beta_i \Delta g_i)^T}{\langle \Delta g_i, \Delta x_i - \beta_i \Delta g_i \rangle}
\end{align}
$$

#### Note
$$
\beta_{i+1} = \beta_i + \frac{(\Delta x_i - \beta_i \Delta g_i)(\Delta x_i - \beta_i \Delta g_i)^T}{\langle \Delta g_i, \Delta x_i - \beta_i \Delta g_i \rangle}
$$
위 에서 
$$
\langle \Delta g_i, \Delta x_i - \beta_i \Delta g_i \rangle \neq 0
$$
단, 현재는 $k=i$ 에서만 구한 것, 따라서 $k=i-1, \cdots 0$ 에서도 성립함을 증명해야 한다.

### Theorem 
The Matrix $\beta_i$ satisfies Quasi-Newton property i.e.
$$
\beta_{i+1} \Delta g_k = \Delta x_k, \;\;\; k=0, 1, \cdots i-1, i
$$

#### proof
By Induction,
- $\beta_1 \Delta g_0 = \Delta x_0$, by construction
- Suppose that $\beta_k \Delta g_j = \Delta x_j$, $j=0, 1, \cdots k-1$ are satisfied.
- Need to prove that

$$
\beta_{k+1} \Delta g_j = \Delta x_j, \;\;\; j=0, 1, \cdots k
$$
if $j=k$ then by construction that are satisfied.

for $j \leq k-1$
$$
\begin{align}
\beta_{k+1} \Delta g_j = \beta_k \Delta g_j + y_k \langle \Delta x_k - \beta_k \Delta g_k, \Delta g_j \rangle 
\beta_{k+1} = \beta_k + \frac{(\Delta x_k - \beta_k \Delta g_k)(\Delta x_k - \beta_k \Delta g_k)^T}{\langle g_k, \Delta x_k - \beta_k \Delta g_k \rangle}
\end{align}
$$
Let
$$
y_k \triangleq \frac{\Delta x_k - \beta_k \Delta g_k}{\langle g_k, \Delta x_k - \beta_k \Delta g_k \rangle} 
$$
Since $\beta_k \Delta g_i = \Delta x_j$ (by hypothesis) and $\beta_k$ is symmetric and 
$$
\beta_k \Delta g_j = \Delta x_j ,\;\;\; \Delta g_j = \beta_k^{-1} \Delta x_j , \;\;\; \beta_k^{-1} = H 
$$
we can conclude that
$$
\begin{align}
\langle \Delta x_k - \beta_k \Delta g_k, \Delta g_j \rangle &= \langle \Delta x_k, \Delta g_j \rangle - \langle \beta_k \Delta g_k, \Delta g_j \rangle \\
&= \langle \Delta x_k, H\Delta x_j \rangle - \langle \Delta x_k, H\Delta x_j \rangle = 0
\end{align}
$$
Thus, 
$$
\beta_{k+1} = \Delta g_j = \beta_k \Delta g_j = \Delta x_j
$$
**Q.E.D**

**Rank-1 test method requires that $\langle \Delta g_k, \Delta x_k - \beta_k \Delta g_k \rangle \neq 0 $**
이러한 단점을 보완하기 위하여 Rank-2 test model이 개발 되었다.

#### Note
다시말해 rank-one Method는 $\beta_{i+1} = \beta_i + \alpha_i z_i z_i^T$ 를 의미하여
- $z_i = \Delta x_i - \beta_i \Delta g_i$
- $\alpha_i = (\langle \Delta g_i, \Delta x_i - \beta_i \Delta g_i \rangle)^{-1}$ 

을 의미한다.


### Rank Two Method
In rank one method
$$
\begin{align}
\beta_{i+1} &= \beta_i + \alpha_i (\Delta x_i - \beta_i \Delta g_i)(\Delta x_i - \beta_i \Delta g_i)^T \;\;\; \alpha_i \in \mathbb{R} \\
&= \beta_i + \alpha_i \Delta x_i \Delta x_i^T - \alpha_i (\beta_i \Delta g_i \Delta x_i ^T + \Delta x_i (\beta_i \Delta g_i)^T)
+ \alpha_i \beta_i \Delta g_i (\beta_i \Delta g_i)^T
\end{align}
$$
여기에서 다음은 Symmetric 이다.
- $\beta_i$ 
- $\Delta x_i \Delta x_i^T$ 
- $(\beta_i \Delta g_i \Delta x_i ^T + \Delta x_i (\beta_i \Delta g_i)^T)$
- $\beta_i \Delta g_i (\beta_i \Delta g_i)^T$

그러나 다음 항은 Symmetric이 아니다.
- $\beta_i \Delta g_i \Delta x_i ^T $ 
이 항은 대칭이 되는 다른 항을 더하였기 때문에 Symmetric이 된다. (위에서 세번째 항목)

#### Idea
Supress the non-symmetric terms, and let
$$
\beta_{i+1}^{DFP} \triangleq \beta_i + \beta_i \Delta x_i \Delta x_i^T + \gamma (\beta_i \Delta g_i)(\beta_i \Delta g_i)^T
$$
it is invented by Davison, Fletcher, Powell .. 그래서 DFP 법이라고 한다.

Since it has to satisfy Quasi-Newton method property, i.e. $\beta_{i+1} \Delta g_i = \Delta x_i$ 
$$
\Delta x_i = \beta_i \Delta g_i + \beta_i \Delta x_i \Delta x_i^T \Delta g_i + \gamma_i (\beta_i \Delta g_i)(\beta_i \Delta g_i)^T \Delta g_i
$$

Pick 
$$
\beta_i = \frac{1}{\langle \Delta x_i, \Delta g_i \rangle}, \;\;\; \gamma_i = \frac{-1}{\langle \beta_i \Delta g_i, \Delta g_i \rangle}
$$

여기서 $\langle \beta_i \Delta g_i, \Delta g_i \rangle​$ 은 0이 되지 않는다. ($\Delta g_i = 0​$이면 최적점 이다.)
그리고 $\langle \Delta x_i, \Delta g_i \rangle​$ 은 0이 될 가능성이 극히 작다. ($\Delta x_i​$ 와 $\Delta g_i​$가 Orthogonal 한 경우? )

### DFP : Variable Metric Algorithm


| Procesdure | Processing|
|---|---|
| Data | $x_o \in \mathbb{R}^n$ |
|| $B_0$: a Symmetric positive definite matrix $n \times n$ ex) $I$ |
| Step 0 | Set $i=0$ |
| Step 1 | If $g_i = 0$ stop else continue |
|        | Step Size Rule :  |
|        | $\lambda_i = \arg \min f(x_i - \lambda \beta_i g_i$) |
| Step 2 | Update |
|        | $x_{i+1} = x_i - \lambda_i \beta_i g_i$       |
|        | $\Delta x_i = x_{i+1} - x_i $ |
|        | $\Delta g_i = g_{i+1} - g_i $ |
|        | $\beta_{i+1} = \beta_i + \frac{1}{\langle \Delta x_i , g_i \rangle} \Delta x_i \Delta x_i^T - \frac{(\beta_i \Delta g_i)(\beta_i \Delta g_i)^T}{\langle \Delta g_i, \beta_i \Delta g_i \rangle }$|
| Step 3 | Set $i=i+1$ and goto step 1 |

#### Results
Suppose that $f(x) = \frac{1}{2} \langle x, Hx \rangle + \langle d, x \rangle $ with $H$ a symmetric positive definite $n \times n$ matrix.

1. If $\beta_i$ is a symmetric positive definite matrix then $\beta_{i+1}$ is a symmetric positive definite matrix
2. $\beta_{i+1} \Delta g_k = \Delta x_k$, $k=0, 1, \cdots, i$ ($\beta_n = H^{-1}$)
3. $x_{n+1}$ is a minimizer of $f(\cdot)$
4. $\{ \Delta x_i \}_{i=0}^{n-1}$ are H-conjugate i.e. $\langle \Delta x_i, H\Delta x_j \rangle = 0$ for $i \neq j$

**1**
$$
\beta \Delta G = \Delta X \;\;\; \because \beta = H^{-1}
$$

**2**
$$
\Delta G = \beta^{-1} \Delta X = H \Delta X 
$$

The difference between **1**, and **2** 
$$
\beta \leftrightarrow H, \;\;\; \Delta g_i \leftrightarrow \Delta x_i \;\;\text{(duality holds)}
$$
Since we have
$$
\beta_{i+1} = \beta_i + \frac{\Delta x_i \Delta g_i^T}{\langle \Delta x_i, \Delta g_i \rangle} - \frac{(\beta \Delta g_i)(\beta \Delta g_i)^T}{\langle \Delta g_i, \beta_i \Delta g_i}
$$
by duality, we can estimate the Hessian $H$ by

$$
H_{i+1} = H_i + \frac{\Delta g_i \Delta g_i^T}{\langle \Delta g_i, \Delta x_i \rangle} - \frac{(H_i \Delta x_i)(H_i \Delta x_i)^T}{\langle x_i , H_i \Delta x_i \rangle}
$$

**Duality **
$$
\beta_i \rightarrow H_i \;\;\; \Delta g_i \rightarrow \Delta x_i \;\;\; \Delta x_i \rightarrow \Delta g_i
$$

But $x_{i+1}$ is updated by
$$
x_{i+1} = x_i - \lambda_i H_i^{-1} g_i \;\;\; \text{i.e.} \;\;\; H_i^{-1} \beta_i
$$
is needed 

Since 
$$
(A + ab^T)^{-1} = A^{-1} - \frac{(A^{-1}a)(b^T A^{-1})}{1 + b^T A^{-1} a}
$$
위에서 $H$의 Inverse를 생각해 보면
$$
H_{i+1} = C_i - \frac{(H_i \Delta x_i)(H_i \Delta x_i)^T}{\langle \Delta x_i, H_i \Delta x_i \rangle}
$$
의 Inverse 와 
$$
C_i = H_i + \frac{\Delta g_i \Delta g_i^T}{\langle \Delta g_i, \Delta x_i \rangle}
$$
의 Inverse를 생각할 수 있다.

(Matrix Inversion Lemma 에 의하여 ... 각각을 만들어 보면)

We can obtain $\beta_{i+1} = H_{i+1}^{-1}$ so that
$$
\beta_{i+1}^{BFGS} = \beta_i + \left( \frac{1 + \Delta x_i^T \beta_i \Delta x_i}{\langle \Delta x_i, \Delta g_i \rangle}\right) \frac{\Delta g_i \Delta g_i^T}{\langle \Delta g_i, \Delta x_i \rangle} - \frac{\Delta g_i \Delta x_i^T \beta_i + \beta_i \Delta x_i \Delta g_i^T}{\langle \Delta x_i, \Delta g_i \rangle}
$$

... invented by Broyden, Fletcher Goldfard Shannon
**BFGS Method**

### Broyden Family
$$
\beta_{i+1}^{\phi} = \phi_i \beta_{i+1}^{DFP} + (1 - \phi_i) \beta_{i+1}^{BFGS}
$$


