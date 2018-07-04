---
layout: post
title:  "FirstPhase"
date:   2018-07-04 14:49:00 +0900
categories:
  - Differential Geometry
tags:
  - Differential Geometry
  - Fundamental
  - Theories
comments: true
---

Differential Geometry [1]
=====================
{:.no_toc}

* Table of Contents
{:toc}

## Directional Derivatives

### Definition 3.1
Let $f$ be a differential real-valued function on $\mathbb{R}^3$ and let $v_p$ be a tangent vector to $\mathbb{R}^3$.
Then the number
$$
v_p[f] = \frac{d}{dt}f(p+tv) |_{t=0}
$$
is called **the derivative of $f$** with respect to $v_p$.

$v_p[f]$ is a **directional derivative**
Alternative form : $v_p(f)$
Another form (see 1 Form): $df(v_p)$

### Lemma 3.2
If $v_p = (v_1, v_2, v_3)_p$ is a tangent vector to $\mathbb{R}^3$, then
$$
v_p(f) = \sum v_i \frac{\partial f}{\partial x_i}(p) = \left< v_p, \nabla f \right>
$$

#### proof of Lemma 3.2

Let $p=(p_1, p_2, p_3)$ then
$$
p+tv = (p_1+tv_1, p_2+tv_2, p_3+tv_3)
$$
we use the chain rule to compute the derivative at $t=0$ of the function
$$
f(p+tv)=f(p_1+tv_1, p_2+tv_2, p_3+tv_3).
$$
Since

$$
\frac{d}{dt}(p_i + tv_i) = v_i
$$
We obtain
$$
v_p[f]=\frac{d}{dt}f(p+tv)|_{t=0} \;\;\;\;\;  \text{by Definition 3.1}
$$
$$
\frac{d}{dt}f(p+tv)|_{t=0} = \sum\frac{df(p+tv)}{d(p+tv_i)}\cdot \frac{d(p+tv_i)}{dt} |_{t=0} = \sum \frac{\partial f}{\partial x}v_i
$$

### Lemma 1.4.6
Let $\alpha$ be a curve in $\mathbb{R}^3$ and let $f$ be a differentiable function on $\mathbb{R}^3$. Then
$$
\alpha'(t)[f] = \frac{df(\alpha)}{dt}(t)
$$

생각해 보면 단순 Parameter curve $\alpha(t)$ 가 시간에 대한 변화율을 가지므로, 그럼 스칼라는 미분에 의해 벡터가 된다. 즉, 이 벡터에 대한 위의 Directional Derivative가 된다. 그럼 $f(p)$ 대신 $f(\alpha)(t)$ 가 된다.
점 p 대신 $\alpha(t)$로 치환되는 것

따라서,
$$
\alpha'(t)[f] = \left< \alpha'(t), \nabla f \right> = \sum \frac{\partial f(\alpha (t))}{\partial x}\alpha'(t) = \frac{df(\alpha)}{dt}(t)
$$

By definition, $\alpha'(t)[f]$ is the rate of change of $f$ along the line through $\alpha(t)$ in the $\alpha'(t)$ direction.

## 1-forms

The differential of the $f$
$$
df = \frac{\partial f}{\partial x}dx + \frac{\partial f}{\partial y}dy + \frac{\partial f}{\partial z}dz
$$
이는 마치 이렇게 보인다. $df = \left< dx_i, \nabla f \right>$

### 1 form
$\phi_p : T_p(\mathbb{R}^3) \rightarrow \mathbb{R} $
* 즉, **Tangent Space를 스칼라로 보내는 함수**
* 살펴보면 Tangent vector $v_p$는 $v_p[f]$ 에 의해 Directional Derivative라는 Scalar 값이 된다. 그렇다면, $\left< \cdot, \nabla f \right>$ 를 보다 강조하여 이것을 **Differential 1-form** 이라고 할 수 있겠다.

If $f:\mathbb{R}^3 \rightarrow \mathbb{R}$, and $\phi_p : T_p(\mathbb{R}^3) \rightarrow \mathbb{R}$ then $f\phi$ is 1 form such that
$$
f \phi(v_p) = f(v_p)\phi(v_p) \;\;\; \text{where} \;\; p \in \mathbb{R}^3,\; v_p \in T_p (\mathbb{R}^3)
$$

### Definition 5.1 : Defionition of 1-form
A 1-form $\phi$ on $\mathbb{R}^3$ is **a real-valued function** on the set of all tangent vectors on $\mathbb{R}$ such that $\psi$ is linear at each point, that is
$$
\psi(av+bw)=a\psi(v)+b\psi(w)
$$
for any number $a, b$ and tangent vectors $v, w$ at the same point of $\mathbb{R}^3$.

### Definition 5.2 : Expression of 1-form
For $f:\mathbb{R}^3 \rightarrow \mathbb{R}$, the differential $df$ of $f$ is the 1-form such that
$$
df(v_p) = v_p[f]
$$

### Remind for 1-form
* $df$ 는 $\mathbb{R}^3$ 의 모든 방향으로의 $f$의 변화율, 즉,
$$
df(v_p) = v_p[f] = \left< v_p, \nabla f(p) \right>
$$
* 다음 방정식은 모두 같은 것이다.
$$
df(v_p)=\left< df(p), v_p \right> = v_p[f] = v_p(f),\;\;\; \alpha'(t)[f] = \frac{df(\alpha)}{dt}(t)
$$

### Example of 1-form
* Differential of Elemental cooridinate $x_i$
$$
dx_i(v_p) = v_p[x_i] = \sum_j v_j \frac{\partial x_i}{\partial x_j}(p)=\sum_j v_j \delta_{ij}= v_i
$$
* Differential of Linear combination with 1-form
when $\psi = \sum f_i dx_i$
$$
\psi(v_p) = (\sum f_i dx_i)(v_p) = \sum f_i(p) dx_i(v_p) = \sum f_i(p) v_i
$$

### Corollary 1.5.5 (Property of $df$)
$$
df = \sum \frac{\partial f}{\partial x_i}dx_i
$$

* 만일, 위에서 $f_i$ 를 $\frac{\partial f}{\partial x_i}$ 로 정의하면
  $$
  \psi = \sum f_i dx_i = \sum \frac{\partial f}{\partial x_i} dx_i = df
  $$
따라서 $\psi(v_p) = df(v_p)$

* Tangent vector $v_p \in T_p(\mathbb{R}^3)$ 은 Example of 1-form에 따라서 다음과 같이 이루어진 것으로 본다.
$$
v_p = \sum_j v_j(p) \frac{\partial}{\partial x_j}
$$

### Lemma 1.5.7 : 합성함수의 Differential Form
For $h \in \mathbb{R}$ and $f \in \mathbb{R}$,
$$
d(h(f))=h'(f)df
$$
#### proof of Lemma 1.5.7
Simple Chain Rule :
$$
\frac{\partial h(f)}{\partial x} = \frac{\partial h(f)}{\partial f}\frac{\partial f}{\partial x} = h'(f)\frac{\partial f}{\partial x}
$$
Thus,
$$
d(h(f)) = \sum_j \frac{\partial h(f)}{\partial f} \frac{\partial f}{\partial x_j} dx_j = h'(f) \sum_j  \frac{\partial f}{\partial x_j} dx_j = h'(f)df
$$

### Differential Forms
Differential forms 는 **Association** 과 **Distribution** 이 성립되므로 **Group** 이다. 그러나 Commutative는 성립하지 않으므로 Ring 혹은 field는 성립하지 못한다.

### Computation of Wedge Product
* For $\phi = (xdx - ydy), \psi = (zdx + xdz)$
  $$
  \begin{align*}
  \phi \wedge \psi &= (xdx - ydy) \wedge (zdx + xdz)\\
   &= x^2 dx \wedge dz + yz dx \wedge dy -xy dy \wedge dz\\
   &= x^2 dx dz + yz dx dy -xy dy dz
  \end{align*}
  $$
다시말해 Orthogonal Coordinate $dx, dy, dz$ 간의 wedge Product $dx \wedge dy  = dxdy$ 이다. 이는 좌표축의 넓이 라는 측면에서 당연하다.

* For $\theta = zdy, \phi = (xdx - ydy), \psi = (zdx + xdz)$,
  $$
  \begin{align*}
  \theta \wedge \phi \wedge \psi &= zdy \wedge (xdx - ydy) \wedge (zdx + xdz)\\
   &= zdy \wedge (x^2 dx dz + yz dx dy -xy dy dz)\\
   &= -x^2z dxdydz
  \end{align*}
  $$

### Lemma : Differential Form의 순서
If $\phi, \psi$ are 1-forms then

$$
\phi \wedge \psi = - \psi \wedge \phi
$$

#### Proof of Lemma
Let $\phi = \sum f_i dx_i$ and $\psi = \sum g_k dx_k$, then

$$
\begin{align*}
\psi \wedge \phi &= \sum_i f_i dx_i \wedge \sum_k g_k dx_k = \sum_i \sum_k f_i g_k dx_i \wedge dx_k \\
 &= \sum_i \sum_k -f_i g_k dx_k \wedge dx_i = -\phi \wedge \psi
\end{align*}
$$

### Definition : The exterior derivatives
if $ \phi = \sum_i f_i dx_i$ is a 1-form on $\mathbb{R}^3$, the exterior derivative of $\phi$ is the 2-form such that
$$
d\phi = \sum_i df_i \wedge dx_i
$$

#### Meaning if the exteriro derivatives
Let $ \phi = \sum_i f_i dx_i$, then

$$
d\phi = d(\sum_i f_i dx_i) = \sum_i df_i \wedge dx_i = \sum_i \sum_k \frac{\partial f_i}{\partial x_k} dx_k \wedge dx_i
$$

* 생각해보면 만일 3차원이라고 하면 - 값을 가진 Component는 나올 수 없으며 + 의 값을 가진 2개의 Component는 나올 수 있다. 이는 Covariant Derivatives 에서 확실히 보이도록 한다.

### Theorem : Linear Property of exterior derivatives
Let $f, g \in \mathbb{R}$ be functions and $\phi, \psi$ be 1-forms on $\mathbb{R}^3$.

$$
\begin{align*}
d(fg)    &= df g + f dg\\
d(f\phi) &= df \wedge \phi + f d\phi\\
d(\phi \wedge \psi) &= d\phi \wedge \psi - \phi \wedge d\psi
\end{align*}
$$

#### proof of Theorem
처음 두 방정식은 자명하므로 증명에서 뺀다.
요는 마지막 방정식의 경우 $\wedge$ 의 영향으로 + 가 아닌 - 가 나타난다는 사실이다. 쉽게 생각하면

- 첫번째 미분은 **첫항에 작용하므로 부호가 변하지 않지만,**
- 두번째 Exterior Derivative는 **두번째항에 적용되기 때문에 부호가 (-)가 된다는 의미이다.** 이를 증명한다.

Let $\phi = f dx$ and $\psi = g dy$ then
$$
d\phi \wedge d\psi = d(fg dxdy)= d(fg) dxdy = \left(\frac{\partial fg}{\partial z}dz \right) dxdy = \left( f \frac{\partial g}{\partial z} + g \frac{\partial f}{\partial z} \right) dxdydz
$$
$$
d\phi \wedge \psi = d(f dx) \wedge g dy = g df \wedge dx \wedge dy = g\frac{\partial f}{\partial z} dz \wedge dx \wedge dy = g\frac{\partial f}{\partial z} dx dy dz
$$
$$
\phi \wedge d\psi = fdx \wedge d(gdy)= fdx \wedge dg \wedge dy = fdx \wedge \frac{\partial g}{\partial z}dz \wedge dy = f\frac{\partial g}{\partial z} dx \wedge dz \wedge dy = -f\frac{\partial g}{\partial z} dxdydz
$$

따라서, $ d(\phi \wedge \psi) = d\phi \wedge \psi - \phi \wedge d\psi $
이는 앞에서 + 의 값을 가진 2개의 Component가 나오게 하기 위하여 두번째 항에 대한 Exterior Derivative 가 (-)가 되는 것이다.  

## Covariant Derivatives
### Definition : Covariant Derivatives
Let $W(p)$ be a  vector field on $\mathbb{R}^3$, and let $v$ be a tangent vector field to $\mathbb{R}^3$ at the point $p$ . Then the ** covariant derivative ** of $W(p)$ with respect to $v$ is the tangent vector

$$
\nabla_v W = W(p+tv)'(0)
$$

$\nabla_v W$ measures **the initial rate of changes** of $W(p)$ **as p moves in the $v$ direction**.

### Lemma : Computation of Covariant Derivative
If $ W = \sum w_i U_i $ is a vector field on $\mathbb{R}^3$ and $v$ is a tangent vector at $p$, then
$$
\nabla_v W = \sum v[w_i] U_i (p)
$$

#### proof of Lemma
$$
W(p+tv) = \sum w(p+tv)U_i(p+tv)
$$
By definition
$$
\nabla_v W = W(p+tv)'(0) = \sum w(p+tv)' U_i(p+tv)|_{t=0}
$$
By definition of $w(p+tv)'(0) = v[w_i]$  the lemma is proved (Q.E.D)

It means that

$$
\nabla_v W = \sum v[w_i] U_i = \sum \left< dw_i, v\right> U_i = \sum dw_i(v) U_i
$$

### Linearity of Covariant Derivative
$$
\nabla_v (fY)(p) = v[f]Y(p) + f \nabla_v Y(p) = df(v)Y(p) + f \nabla_v Y(p)
$$

### Note : Basic Identify of $U_i$

$$
U_i [f] = \frac{\partial f}{\partial x_i}
$$

### Example : Covariant of Vector Field
$$
\begin{align*}
V &= (y-x)U_1 + xy U_3\\
W &= x^2 U_1 + yz U_3
\end{align*}
$$

#### Solution
$\nabla_v W$를 구하기 위해 먼저 $dw_k (v) = v[w_k]$ 를 구해야 한다.

$$
dw_1 = 2x U_1, dw_2 = 0, dw_3 = z U_2 + y U_3
$$

$$
\begin{align*}
v[w_1] &= dw_1(v) &= 2x(y-x) \\
v[w_2] &= dw_2(v) &= 0 \\
v[w_3] &= dw_3(v) &= xy^2 \\
\end{align*}
$$

$$
\nabla_V W = 2x(y-x)U_1 + xy^2 U_3
$$
