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

식 (1)을 $x$ 에 대하여 미분하고 $\nabla f(x) = 0$ 으로 놓은 후 $x \rightarrow x_{p+1}, \; a \rightarrow x_p$로 놓으면 다음과 같다.

$$
\begin{aligned}
0 &\approx \nabla f(x_p) + H(x_p)(x_{p+1} - x_p) \\
&\Rightarrow x_{p+1} = x_p - H^{-1}(x_p) \nabla f(x_p) 
\end{aligned}
\tag{4}
$$

이는 $h_p \equiv 1$ and $B = -H^{-1}(x_p)$ 이다. 이를  **different metric**에 의한 steepest ascent 방법으로 간주한다.

#### Note : Different Metric Method 
Euclidean Metric에서 $x$ 에서 $y$의 거리는 $\langle x-y, x-y \rangle^{\frac{1}{2}}$ 이다. 
Distance from x to y in the Euclidean metric is $\langle x-y, x-y \rangle^{\frac{1}{2}}$. 
If $B$ is a positive definite matrix, it is possible to define a new distance measure by $\langle x-y, B(x-y) \rangle^{\frac{1}{2}}$ 

따라서 만일, $\langle x - x_0, B( x - x_0) \rangle^{\frac{1}{2}} = k^2$ 이면 Center $x_0$ 인 타원 평면에 거리가 정의된다.  


식 (3)이 Exact 이면 $f(x)$ 는 Quadratic polynomial 이고 Newton's method yields the maximum in one step. However, if $f(x)$ is not exact in (3), it has an approximation to the  the maximum which is sufficiently close to it, then it may be expected to be a very ** good approximation**. 

하지만, step size $h_p$ 가 너무 크다던가, $H(x)$ 가 Negative definite 라면, 제대로 된 Search가 어렵다. (당연한 것 )

이에 대하여 본 논문은 같은 Quadratic Approximation을 사용하는데, Quadratic Approximation이 잘 되면 Step size를 중가 시키고 잘 되지 못했다면, step size를 줄이는 방식이다. 
In this paper, a new method which uses the same quadratic approximation, including a parameter which limits the step size. This parameter is altered according to the apparent accuracy of the quadratic approximation so that the step size is increased in region where the approximation is good and cut down in regions where it is bad.

## Restricted Maximization of a Quadratic Function

Consider a quadratic function $f^Q(x)$, and the matrix $H$ is then constant. (Quadratic 이면 당연 !!) The expansions (3) and (4) are exact. (역시 Quadratic 이면 당연) 

식 (4) 에서, 만일 $H$ 가 non-singular 이면

$$
c = a - H^{-1} \nabla f(a)

\tag{5}
$$

is the unique point where $\nabla f(x) = 0$ 그리고 $H < 0$ 이면 $f^Q(x)$는 unique global minimum을 $c$에서 가지게 된다. 

### Lemma 1 

Let $\alpha$ be any number such that $H - \alpha I$ is negative definite, and define

$$
b_{\alpha} = a - (H - \alpha I)^{-1} \nabla f(a)
\tag{6}
$$

$$
r_{\alpha} = \| b_{\alpha} - a \|
\tag{7}
$$

then $f^Q(b_{\alpha}) \geq f^Q(x)$ for all $x$ such that $\| x - a \| = r_{\alpha}$.

#### proof

Set an exact quadratic function $f^Q(x)$ such that

$$
f^Q(x) = f^Q(a) + \langle \nabla f^Q(a), x - a \rangle + \frac{1}{2} \langle x - a, H(x-a) \rangle
$$

Consider the quadratic function

$$
\begin{aligned}
f^R(x) 

&= f^Q(a) + \langle \nabla f^Q(a), x - a \rangle + \frac{1}{2} \langle x - a, (H - \alpha I)(x-a) \rangle \\

&= f^Q(a) + \langle \nabla f^Q(a), x - a \rangle + \frac{1}{2} \langle x - a, H(x-a) \rangle - \frac{1}{2} \alpha \langle x-a, x-a \rangle \\

&= f^Q(x) - \frac{1}{2} \alpha \| x - a \|^2
\end{aligned}
$$

Since $H - \alpha I < 0$ is negative definite, (5) with $H$ replaced by $H - \alpha I$ applies to show that $f^R(x)$ has a global maximum at $b_{\alpha}$. Thus for all $x$

$$
f^R(b_{\alpha}) = f^Q(b_{\alpha}) - \frac{1}{2} \alpha \| b_{\alpha} - a \|^2 \geq f^Q(x) - \frac{1}{2} \alpha \|x - a \|^2 = f^R(x)
$$

and if 

$$
\| x - a \| = r_{\alpha} = \| b_{\alpha} - a \|
$$

then $f^Q(b_{\alpha}) \geq f^Q(x)$ , as asserted.

### Lemma 2
If $\nabla f(a) \neq 0$ then the $r_{\alpha}$ defined (6), (7) is a strictly decreasing dunction of $\alpha$ on the interval $(\lambda_1, \infty)$ where $\lambda_1$ is the maximum eigrnvalue of H.

#### proof
From (6), (7)

$$
r_{\alpha} = \| (H - \alpha I)^{-1} \nabla f(a) \|
$$

and application of (A-4) in the Appendix with $H$ replaced by $(H - \alpha I)^{-1}$ yields 

$$
r^2_{\alpha} = \sum_{i=1}^n c_i^2 (\lambda_i - \alpha)^{-2}
\tag{8}
$$

where $c_1 \cdots c_n$ 은 certain constants 이고 $\lambda_1 \geq \lambda_2 \geq \cdots \geq \lambda_n$은 Eigenvalues of $H$ 이다.

이떄, $\forall i, \;\; \lambda_i < \alpha$, 이므로 (8)은 $\alpha$에 대하여 Decreasing function.
**Q.E.D**

### Theorem
Let $\alpha, b_{\alpha}$, and $r_{\alpha}$ be as in Lemma 1, let $B_{\alpha}$ be the region consisting of all $x$ such that $\| x - a \| \leq r_{\alpha}$, and suppose $\nabla f(a) \neq 0$. Then the maximum value of $f^Q(x)$ on $B_{\alpha}$ is attained at $b_{\alpha}$ if $\alpha \geq 0$, and is attained at $b_0$ if $\alpha < 0$. (In this case $b_0$ is interior to the region $B_{\alpha}$)

#### Note of theorem  
본 증명은 너무나 직관적임. 따라서 요약하지 않기로 함.
일단, Exact Quadratic 이면 Maximum Value는 $\| x - a \| \leq r_{\alpha}$ 임을 의미 .  여기서 $x$는  $x_{p+1} = \arg \max_{x} f^Q(x)$ 가 된다. (실제로는 이렇게 되지 않겠지만) 

$r_{\alpha} = \| (H - \alpha I) \|$ 임에도 이렇게 된다는 것은 매우 중요하다. 

### Lemma 3 
If $\nabla f(a) = 0$, then the maximum value of $f^Q(x)$ on the region $B_r$ consisting of all $x$ with $\| x - a \| \leq r$ occurs at $a \pm ru_1$ if $\lambda_1$. (The maximum eigenvalue of $S$) is positive, and at $a$ otherwise. (Here $u_1$ is a unit eigenvector associated with $\lambda_1$

#### Note of Lemma 3
**해당 Lemma의 증명도 자명하여 그냥 받아들이기로 함**
Since the proof of the Lemma 3 is so trivial, that we accept it as true proposition.

위의 Theorem 에서 이미 보였지만, $\arg \max_{x} f^Q(x) = x_{p+1}$ 이 될 수 있음을 보였다. 
이를 보다 엄밀하게 설명한 것이 Lemma 3 이다. 즉, $x^* = \arg{x} \nabla f^Q(x) = 0$ 인 $x^* \in B^o(a, r_{\alpha})$ 임을 설명한 것이다.
As the above theorem already shows, it is true proposition that $\arg \max_{x} f^Q(x) = x_{p+1}$. The lemma 3 illustrates the meaning of theorem rigorously. In other words, it establish that if  $x^* = \arg{x} \nabla f^Q(x) = 0$ then $x^* \in B^o(a, r_{\alpha})$.  

### Implementation of the algorithm

#### $\nabla f(x_p) \neq 0$ : Significantly different from 0

이 경우 다음과 같이 놓는다.

$$
\alpha = \lambda_1 + R \| \nabla f(x_p) \|
$$

where $\lambda_1$ is the largest eigenvalues of $H$, and $R$ is a **positive parameter** 
Take
$$
x_{p+1} = x_p - (H(x_p) - \alpha I)^{-1} f(x_p)
\tag{9}
$$

$$
x_{p+1} = x_p - H^{-1}(x_p) f(x_p)
\tag{10}
$$

Lemma와 Theorem에서 $x_{p+1} \in B^o(x^p, \|(H(x_p) - \alpha I)^{-1} \nabla f(x_p) \|$ 이면 **the maximum of the quadratic approximation** .

- Lemma 2 에서 보듯, $\alpha$ 가 크다는 것은 $R$이 크다는 것이고 그에따라 $B_{\alpha} = B^o(x^p, \|(H(x_p) - \alpha I)^{-1} \nabla f(x_p) \|$ 는 $\alpha$가 커짐에 따라  
- Eigenvalue of $(H(x_p) - \alpha I)^{-1} $ 는  ($H(x_p) $ 의 Eigenvalue는 $\lambda_i$ 이므로 )
$$
\mu_i = \frac{-1}{\lambda_1 + \| \nabla f(x_p) \| R - \lambda_i} \;\;\; \forall i \in \mathbf{Z}[1, n]
$$

위에서 논한대로 $H$의 Eigenvalue 들이 $\lambda_i$ 이면 $H - \alpha I$의 Eigenvalue는 $\lambda_i - \alpha$가 된다. 특히 만일 $H - \alpha I$이 Negative definite 이면  $\lambda_i - \alpha \Rightarrow \alpha > \lambda_i$ 이다. 
따라서 가장 큰 $u_i$의 절대값은 $\| u_i \| = (\| \nabla f(x_p) \| R)^{-1}$ 이다. 그러므로 $B_{\alpha}$ 의 radius는 
$$
\| (H(x_p) - \alpha I)^{-1} \nabla f(x_p) \| \leq (\| \nabla f(x_p) \| R)^{-1} \| \nabla f(x_p) \| = R^{-1}
$$

만일, $R$이 매 step 마다 Update 된다고 가정하면, 알고리즘이 Quadratic Maximum 근처에 접근하면 Step Size는 증가하게 되고, 반대로 멀어지면 Step Size는 줄어드는 방식이 된다. [8]

#### $\nabla f(x_p) \approx 0$ : near maximum

이 경우에는 step size가 a preset tolerance of 0 에 위치해 있으므로 만일, $H(x_p)$가 Negative Definite이면 Process는 중단되고 $x_p$는 Maximum value가 될 것이다.

만일 negative definite이 아니라면 이는 Saddle point이므로 Lemma 3이 적용될 것이며 **Step **은 $\lambda_1$에 비례하는 Eigen Vector에 따라 움직이게 될 것이다. 

#### Brief : Final Algorithm

그러므로 어떤 적절한 step size $h(x_p) \in \mathbf{R}$를 도입하면 다음과 같은 Search 방정식을 얻을 수 있다.
Therefore, if we introduce an appropriate scalar step size such as $h(x_p) \in \mathbf{R}$, we can obtain the following search equation:

$$
x_{p+1} = x_p - h(x_p)(H(x_p) - \alpha I)^{-1} \nabla f(x_p)
$$

이떄, $h(x_p)$는 Armijo Rule이나 Golden Search등을 사용하면 된다.

## Conclusion 

본 논문을 살펴본 이유는 본 논문이 Hill-Climbing 특징을 서술하고 있기 때문이며 그 원인은 다음과 같은 Rank-1 Method를 사용하고 있기 때문이다. 

### Brief 
Lemma-1 에서

$$
f^R(x) 
= f^Q(a) + \langle \nabla f^Q(a), x - a \rangle + \frac{1}{2} \langle x - a, H(x-a) \rangle - \frac{1}{2} \alpha \langle x-a, x-a \rangle
$$

로 놓았다.  $f^R(x)$ 를 0에 대하여 미분하고 $\nabla f^R(x) = 0$ 이라 하면.

$$
0 = \nabla f^R(x) 
= \nabla f^Q(a) + H(x-a) - \alpha (x-a)
$$

여기에서 

$$
-\nabla f^Q(a)= (H - \alpha I)(x-a) \Rightarrow x = a - (H - \alpha I)^{-1}\cdot \nabla f^Q(a)
$$
으로 접근한 것이 본 논문이다.

즉,  $H(x_p)$ 대신

$$
(H(x_p) - \alpha I)^{-1}
$$

이에 의해 $x_p$ 주변의 적절한 Radius를 가정하기 위해 다음과 같이 $\alpha$를 놓았다.

$$
\alpha = \lambda_1 + R \| \nabla f(x_p) \|
$$

이에 의해 탐색 영역의 Radius는 

$$
\| (H(x_p) - \alpha I)^{-1} \nabla f(x_p) \| \leq (\| \nabla f(x_p) \| R)^{-1} \| \nabla f(x_p) \| = R^{-1}
$$

의 영역을 가지게 되고 $x_{p+1}$이 다음의 조건을 만족하게 되면 

$$
x_{p+1} \in B^o(x^p, \|(H(x_p) - \alpha I)^{-1} \nabla f(x_p) \|
$$

Maxima를 찾을 수 있다는 의미이다. 고로,  $x_p$ 점에서 정확한 Newton-Rapson 법에 의한 Search가 아니라 하더라도 위의 조건을 만족하는 $\alpha$의 값이 정의되면 이에 종속적인 영역내에 $x_p$가 있기만 해도 Maxima를 찾을 수 있음을 의미한다.

### My Comment 

위에서 $R$ 를 다음과 같이 factorizing 시키면 

$$
R^{-1} = \varepsilon^{-1} - (\varepsilon + 1)^{-1}
$$

이렇게 놓으면 $R = \varepsilon ( \varepsilon + 1)$ 이 된다. 이에 따라 

$$
\| (H(x_p) - \alpha I)^{-1} \nabla f(x_p) \| \leq (\| \nabla f(x_p) \| R)^{-1} \| \nabla f(x_p) \| = (\| \nabla f(x_p) \| (\varepsilon^2 + \varepsilon))^{-1} \| \nabla f(x_p) \| = \frac{1}{\varepsilon} - \frac{1}{\varepsilon + 1}
$$

따라서 $\alpha$ 를 다음과 같이 쓸 수 있다. 

$$
\alpha = \lambda_1 + \varepsilon(\varepsilon + 1) \| \nabla f(x) \| = \lambda_1 + \varepsilon^2 \| \nabla f(x) \| + \varepsilon \| \nabla f(x) \|
$$

그런데 $R > 1$ 이어야 하므로 ($0 < R^{-1} < 1$)에서 $R \approx \varepsilon^2$ 그러므로 다음과 같이 Factorization 한다.

$$
\bar{a} = \lambda_1 + \varepsilon^2 \|\nabla f(x) \|, \;\;\; \beta = \varepsilon \| \nabla f(x) \|
$$

이에 따라, 

$$
(H - (\bar{a} + \beta) I)^{-1} = \left( (H - \bar{a}I) - \beta I\right) = (A - \beta I)^{-1}
$$

where $A = H - \bar{a}$. 여기에 Simple Matrix Inversion Lemma를 적용하면

$$
\begin{aligned}
(A - \beta I)^{-1} &= (-\beta)^{-1} (I - \beta^{-1} A) \\

&= (-\beta)^{-1} \left( I + (I - \beta^{-1} A)^{-1} \beta^{-1} A \right)\\
&= (-\beta)^{-1} \left( I + (\beta I - A)^{-1} \right) = (-\beta)^{-1} I + (-\beta)^{-1} (\beta I - A)^{-1} \cdot A \\
&= (A - \beta I)^{-1} \beta^{-1} A - \beta^{-1}I
\end{aligned}
$$

따라서, 

$$
\begin{aligned}
\|(A - \beta I)^{-1} \nabla f(x) \| &\leq \left\| (A - \beta I)^{-1} \beta^{-1} A - \beta^{-1}I \right\| \cdot \| \nabla f(x) \| \\

&\leq \left( \left\| (A - \beta I)^{-1} \beta^{-1} A \right\| + \| \beta^{-1} \|  \right) \cdot \| \nabla f(x) \| \\

& \leq \left( \| (A - \beta I)^{-1} \| \cdot \| A \| \cdot \|\beta^{-1}\| + \| \beta^{-1} \| \right) \cdot \| \nabla f(x) \| \\

&= (\| (A - \beta I)^{-1} \| \cdot \| A \| + 1) \|\beta^{-1}\| \cdot \| \nabla f(x) \| \\
&= (\| (A - \beta I)^{-1} \| \cdot \| A \| + 1) \cdot \varepsilon^{-1} \\
&\leq (\| \nabla f(x) \| R)^{-1} \varepsilon \| \nabla f(x) \| + \varepsilon^{-1}  \;\;\;\because \|A\| = \varepsilon^2 \| \nabla f(x) \| \\
&= R^{-1} \varepsilon + \varepsilon^{-1} = \varepsilon \cdot \left( \frac{1}{\varepsilon} - \frac{1}{\varepsilon + 1} \right) + \frac{1}{\varepsilon} \\
&= 1 - \frac{\varepsilon}{\varepsilon + 1} + \frac{1}{\varepsilon} = R
\end{aligned}
\tag{11}
$$

식 (11) 에서, $\varepsilon \rightarrow \infty$ 이면 

$$
\lim_{\varepsilon \rightarrow \infty} \|(A - \beta I)^{-1} \nabla f(x) \| = 1 - 1 - 0 = 0
$$

Exact한 경우에 해당된다.
그런데,  Exact한 경우에 대하여 $R$ 혹은 $\frac{1}{\varepsilon} - \frac{1}{\varepsilon + 1}$ 만큼의 차이가 존재하기 때문에 이만큼의 Error 혹은 Hill-Climbing 요소가 있다고 생각할 수 있다. 

이를 사용하여, Stochastic 한 성분이 존재하고 있다고 보면,  이후** Stochastic Analysis를 적용하여 해석할 수 있다. 이는 이후에 생각하기로 한다.** (해석 하는 방법론이 같다.)

#### Note : Simple Matrix Inversion Lemma

$$
\begin{aligned}
(I - a^{-1} P)^{-1} 
&= I + (I - a^{-1} P)^{-1} a^{-1} P \\
&= I + (a \cdot I - P)^{-1} P \;\;\;\;\; a \in \mathbf{R}
\end{aligned}
$$

## Appendix : Property of Eigenvalue and Eigenvectors corresponding to a Symmetry Matrix 

For real symmetric $n \times n$ matrix $H$, there exist $n$ eigenvalues  $ \lambda_1 \geq \lambda_2 \geq \cdots \geq \lambda_n$ and $n$ mutual orthogonal unit vectors (Eigenvectors) $u_1, u_2, \cdots u_n$. 즉,

$$
H u_i = \lambda_i u_i
\tag{A1}
$$


이때, Symmetric Matrix의 Eigenvector 가 Orthogonal 이므로 임의의 벡터 $x$는 다음과 같이 Eigenvector의 Linear Combination이 된다.

$$
x = \sum_{i=1}^n c_i u_i \;\;\; \text{where } c_k \in \mathbf{R}
\tag{A2}
$$

그러므로 임의 Quadratic function $\langle x, Hx \rangle$은 따라서 

$$
\begin{aligned}
\langle x, Hx \rangle 

&= \langle \sum_i c_i u_i, H \sum_j c_j u_j \rangle 
= \langle \sum_i c_i u_i, \sum_j c_j H u_j \rangle \\
&= \langle \sum_i c_i u_i, \sum c_j \lambda_j u_j \rangle 
= \sum_j \lambda_j \langle \sum_i c_i u_i, c_j u_j \rangle \\
&= \sum_j \lambda_j c_j^2 \delta(i-j) 
= \sum_i \lambda_i c_i^2
\end{aligned}
\tag{A3}
$$

또한

$$
\|x\|^2 = \langle x, x \rangle = \sum_i^n c_i^2
$$

이때, $x$가 unit vector라고 하면 $\sum_i c_i^2 = 1$

고로 Unit vector $x$에 대하여 maximum value of $\sum_i^n \lambda_i c_i^2$ 은 $\lambda_1$ 로 놓을 수 있다. 이떄, $c_1 = \pm 1$, $ c_k = 0 $, $\forall k \neq 1$ 이다.  (위의 조건에 부합한다.) 고로

$$
\max_{\| x \| = 1} \langle x, Hx \rangle = \lambda_1
$$

The squared norm of $Sx$ is given by ((A3)에 의해 간단히 유도 된다.)

$$
\| Hx \|^2 = \langle x, H^2 x \rangle = \sum_{i=1}^n \lambda_i^2 c_i^2
\tag{A4}
$$

그런데, $H^2$은 $H$외 갗은 Eigenvalue를 공유하므로ㅓ $\forall x \in \mathbf{R}^n$ 에 대하여 다음이 성립한다.

$$
\| Hx \| \leq \|x\| \max |\lambda_i|
$$


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
