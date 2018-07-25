---
layout: post
title:  "Differential Forms Essential"
date:   2018-07-04 14:49:00 +0900
categories: [Mathematics, Differential Geometry]
tags:
  - Differential Geometry
  - Differential Forms 
comments: true
---

* Table of Contents
{:toc}

## Diffential forms in $\mathbb{R}^n$

### Defintion 1.
A field of linear forms (or exterior form of degree 1) in $\mathbb{R}^3$ is a map $w$ that associates to each $p \in \mathbb{R}^3$ an element $w(p) \in (\mathbb{R}_p^3)^*$ ; $w$ can be written as

$$
w(p) = a_1(p)(dx_1)_p + a_2(p)(dx_2)_p + a_3(p)(dx_3)_p \\
w = \sum_{i=1}^3 a_i(p)dx_i
$$

Let $\varphi: \mathbb{R}^3 \times \mathbb{R}^3 \rightarrow \mathbb{R}$ be a **bilinear (i.e. $\varphi$ is a linearin each variable)** and **alternate (i.e. $\varphi(v_1, v_2) = - \varphi(v_2, v_1)$)**.

For $\varphi_k \in  (\mathbb{R}_p^3)^* $ and $\varphi_1 \wedge \varphi_2 \in \Lambda^2(\mathbb{R}_p^3)^* $ ,  by setting

$$
(\varphi_1 \wedge \varphi_2)(v_1, v_2) = \det(\varphi_i(v_j))
$$

이 경우 $w(p) \in \Lambda^2 (\mathbb{R}_p^3)^*$, $p \in \mathbb{R}^3$에 대하여 이렇게 쓸 수 있다.

$$
w(p) = a_{12}(p)(dx_1 \wedge dx_2) + a_{23}(p)(dx_2 \wedge dx_3) +a_{13}(p)(dx_1 \wedge dx_3)
$$

$$
w = \sum_{i < j} a_{ij} (dx_i \wedge dx_j) \;\;\; \because dx_i \wedge dx_i =0, \; dx_i \wedge dx_j = - dx_j \wedge dx_i 
$$

- 간단한 증명 Let $\varphi_1 (v_1)= \sum_{i=1} a_i dx_i, \; \varphi_2 (v_2)= \sum_{j=1} b_j dx_j$ ($a_i = \frac{\partial v_1}{\partial x_i}$, $b_j = \frac{\partial v_2}{\partial x_j}$ 로 보자. $v_1, v_2 \in \mathbb{R}$) Then

$$
\begin{align}
(\varphi_1 \wedge \varphi_2)(v_1, v_2) &= (a_1 dx_1 + a_2 dx_2) \wedge (b_1 dx_1 + b_2 dx_2) \\
&= a_1 b_1 dx_1 \wedge dx_1 + a_1 b_2 dx_1 \wedge dx_2 + a_2 b_1 dx_2 \wedge dx_1 + a_2 b_2 dx_2 \wedge dx_2 \\
&= a_1 b_2 dx_1 \wedge dx_2 - a_2 b_1 dx_1 \wedge dx_2 \\
&= \det(\varphi_i(v_j)) dx_1 \wedge dx_2 \\
&= \det(\varphi_i(v_j)) 
\end{align}
$$

- 일반적으로 $\varphi \in \Lambda^k(\mathbb{R}_p^n)^*$ 에 대하여 $\varphi : \underset{\text{k times}}{\underbrace{\mathbb{R}_p^n \times \cdots \mathbb{R}_p^n}} \rightarrow \mathbb{R}$

$$
(\varphi_1 \wedge \cdots \wedge \varphi_k)(v_1, \cdots v_k) =\det(\varphi_i(v_j)), \;\;\; i,j = 1, \cdots, k
$$

- Differential form의 중요한 기능은 Differential Maps하에서 하나의 연산으로 기능한다는 것이다.
	- Let $f : \mathbb{R}^n \rightarrow \mathbb{R}^m$ be a differentiable map.
	- Then **$f$ induces a map $f^*$ that takes k-forms in $\mathbb{R}^m$ into a k-forms in $\mathbb{R}^n$** 
		- 마치 **역함수** 처럼 기능한다. i.e. $f : \mathbb{R}^n \rightarrow \mathbb{R}^m$, $f^* : (\mathbb{R}^m)^* \rightarrow (\mathbb{R}^n)^*$
		- 위 첨자에 별표가 붙는 것으로서 역함수 처럼 기능한다는 것을 알 수 있다.

$$
(f^*w)(p)(v_1, \cdots v_k) = w(f(p))(df_p(v_1), \cdots, df_p(v_k))
$$

- 위에서 공학적인 응용에서는 주로 $m=1$ 즉, $f : \mathbb{R}^n \rightarrow \mathbb{R}$ 보는 응용이 대단히 많다.  (최적화 문제등에서)

- 위 Operation을 다시 생각해보면,

$$
\begin{align}
f^*(\varphi_1 \wedge \cdots \wedge \varphi_k)(v_1, \cdots v_k) &= (\varphi_1 \wedge \cdots \wedge \varphi_k)(df(v_1), \cdots, df(v_k)) \\
&= \det(\varphi_i (df(v_j))) \\
&= \det(f^* \varphi_i (v_j)) \\
&= (f^* \varphi_1, \wedge, \cdots, \wedge f^* \varphi_k)(v_1, \cdots, v_k)
\end{align}
$$

- 위에서 $v_1, \cdots v_k$ 를 굳이 벡터로 보지 않는 것이 좋다. 오히려 위의 Differential Form의 정의상 점 $p$로 보는 것이 좋다. (벡터가 맞지만.. $df_p(v_k)$ 이기 때문에..)
	- $v_k$ 까지 있는 것은 **k-form** 이기 때문이다. 즉, $w(v_1, \cdots, v_k) = (\varphi_1 \wedge \cdots \varphi_k)(v_1, \cdots, v_k) = \det(\varphi_i (v_j))$

### Note
$v(f)$는 표기이고 실제는 $df(v) = \langle \nabla f, v \rangle$ 인 것 처럼 Differential Map에 대한 Form 연산도 마찬가지이다.
즉, $f^* w$는 표기이고 실제는 $w (df)$ 즉 Differential Form의 Inner Product 다시말해 Determinent를 의미한다. 

- 표기법

$p \in \mathbb{R}^n, \; v_1 \cdots v_k \in \mathbb{R}_p^n$ 에 대하여 the differential of the map $f$가  $p$에서 다음과 같이 주어지고,

$$
df_p : \mathbb{R}_{p}^n \rightarrow \mathbb{R}_{f(p)}^m 
$$

$g$가 0-form 이면

$$
f^* (g) = g \circ f = g(f)
$$

- An exterior k-form in $\mathbb{R}^n $ is a map $w$ that associates to each $p \in \mathbb{R}^n$  an element $w(p) \in \Lambda^k(\mathbb{R}_p^n)^*$ 는 다음과 같이 표시된다. **Differential k-form**

$$
w(p) = \sum_{i_1 < \cdots i_k} a_{i_1 \cdots i_k} (p) (dx_{i_1} \wedge \cdots \wedge dx_{i_k})_p, \;\; i_j \in \{ 1, \cdots , n \}
$$

위 식의 간략한 표기는 다음과 같다.
$$
w = \sum_I a_I dx_I
$$

- Differentiable 0-form은 다음과 같은 Differentiable function 을 의미한다.
$$
f:\mathbb{R}^n \rightarrow \mathbb{R}
$$

- Elemental differential form such as $dx_i, dy_j \in (\mathbb{R}^n)^* $ 
에 대한 $f^* dx_i $ 의 경우는 ($y$로 치환해도 같다.) 다음과 같다. 

$$
f^* dx_i (v) = dx_i (df(v)) = d(x_i \circ f)(v) = df_i (v)
$$

### Proposition 
Let a differentiable map $f:\mathbb{R}^n \rightarrow \mathbb{R}^m$ 
and $w, \varphi$ be k-forms on $\mathbb{R}^m$ and $g : \mathbb{R}^m \rightarrow \mathbb{R}$ be a 0-form on $\mathbb{R}^m$. Then:

1. $f^* (w + \varphi) = f^* w + f^* \varphi$
2. $f^* (gw)= f^* (g) f^* (w)$
3. If $\varphi_1 \cdots \varphi_k$ are 1-forms in $\mathbb{R}^m$, then 

$$
f^*(\varphi_1 \wedge \cdots \wedge \varphi_k) = f^* \varphi_1 \wedge \cdots \wedge f^*\varphi_k
$$

### Example : compute $f^* w$
Let $w$ be the 1-form in $\mathbb{R}^2 - (0, 0)$ by

$$
w = - \frac{y}{x^2 + y^2}dx + \frac{y}{x^2 + y^2}dy
$$

Let $U$ be the set in the plane $(r,\theta)$ given by

$$
U = \{ r > 0 : 0 < \theta < 2 \pi \}
$$

and let $f:U \rightarrow \mathbb{R}^2$ be the map

$$
f(r, \theta) = 
\begin{cases}
x &= r \cos \theta \\
y &= r \sin \theta
\end{cases}
$$

그러므로 $f^* w$ 는 $\mathbb{R}^2 - (0, 0)$ 를 $U$로 가져온다.

#### How to
Let $w = \sum_i a_i dx_i$ then

$$
a_1 = - \frac{y}{x^2 + y^2}, \;\; a_2 = \frac{y}{x^2 + y^2}, \;\; dx_1 =dx, \;\; dx_2 = dy
$$

Thus

$$
f^* w = \sum_i f^* a_i f^* dx_i = \sum_i (a_i \circ f) (dx_i (df ))
$$

$f$ 는 Corrdination Transform이므로 $a_i$의 $(x,y)$를 $(r, \theta)$로 변경시켜야 한다.

$$
\begin{align}
a_1 \circ f &= (- \frac{y}{x^2 + y^2}) \circ f(r, \theta) = -\frac{1}{r} \sin \theta \\
a_2 \circ f &= (\frac{x}{x^2 + y^2}) \circ f(r, \theta) = \frac{1}{r} \cos \theta 
\end{align}
$$

그리고 Elementary Differential의 변화는 $dx_i(df) = d(x_i \circ f) = df_i$ 이므로  

$$
\begin{align}
df_1 &= \cos \theta dr - r \sin \theta d\theta \\
df_2 &= \sin \theta dr + r \cos \theta d\theta 
\end{align}
$$

따라서

$$
\begin{align}
f^* w &= (a_1 \circ f) df_1 + (a_2 \circ f) df_2 \\
&= -\frac{1}{r} \sin \theta (\cos \theta dr - r \sin \theta d\theta) + \frac{1}{r} \cos \theta (\sin \theta dr + r \cos \theta d\theta ) \\
&= d \theta
\end{align}
$$

#### Note 1.
$f^*w = w(df)$ 로 생각하면 

$$
f^*w = w(df) = \sum_i^2 (a_i dx_i) (df) = \sum_i^2 (a_i \circ f) (dx_i(df)) = \sum_i^2 (a_i \circ f) df_i 
$$

$f^* w$는 $f: U \rightarrow \mathbb{R}^2$ 이므로 $U$위의 Differential로 정의되어야 하므로 최종적인 형태는 $df_i$의 선형 결합으로 나타나야 한다. 

#### Note 2. : 1-form $w$가 저렇게 주어진 이유
먼저 원호의 길이에 대한 것을 생각해보자 원호의 길이는 보통 **ArcTan**를 사용하여 구하는 것이 일반적이다  왜냐하면, 원호의 각도가 아닌 임의 벡터의 각도를 측정해야 하기 때문이다.

따라서 다음과 같다.

$$
\theta = \tan^{-1} (\frac{y}{x})
$$

그러므로 **ArcTan**의 미분을 정의해야 위 예제의 원호에서의 1-form을 우선 계산할 수 있다. $y = \tan (x)$의 역함수는 $x = \tan^{-1}(y)$ 이므로 $x = \tan (y)$ 로 놓고 $x$에 대하여 미분해보면 

$$
\frac{\partial x}{\partial x} = \frac{\partial}{\partial y} \tan (y) \frac{dy}{dx} = {\sec^2 (y)} \frac{dy}{dx} \\
\frac{dy}{dx} = \frac{1}{\sec^2 (y)} = \frac{1}{1 + \tan^2(y)} = \frac{1}{1 + x} = \frac{d}{dx} \tan^{-1}(x)
$$

따라서 1-form $w$를 다음과 같이 정의한다. 

$$
w = \frac{d}{d(x,y)} \tan^{-1} (\frac{y}{x}) = \frac{\partial }{\partial x} \tan^{-1} (\frac{y}{x}) dx + \frac{\partial }{\partial y} \tan^{-1} (\frac{y}{x}) dy
$$

여기에서 $ u = \frac{y}{x}$ 로 놓으면

$$
w = \frac{d}{du} \tan^{-1} (u) = \frac{\partial }{\partial x} \tan^{-1} (u) dx + \frac{\partial }{\partial y} \tan^{-1} (u) dy
$$

이기 때문에 $u$에 대한 $x, y$의 미분을 구하면

$$
\frac{\partial u}{\partial x} = -\frac{y}{x^2} = -\frac{1}{x} u, \;\;\;  \frac{\partial u}{\partial y} = -\frac{1}{x} 
$$

그러므로

$$
\begin{align}
\frac{\partial}{\partial u}(\tan^{-1} u) \frac{\partial u}{\partial x} &= \frac{1}{1 + u^2} (-\frac{y}{x^2}) = \frac{x^2}{x^2 + y^2} (-\frac{y}{x^2}) = -\frac{y}{x^2 + y^2} \\
\frac{\partial}{\partial u}(\tan^{-1} u) \frac{\partial u}{\partial y} &= \frac{1}{1 + u^2} (\frac{1}{x}) = \frac{x^2}{x^2 + y^2} (\frac{1}{x}) = \frac{x}{x^2 + y^2}
\end{align}
$$

따라서

$$
\begin{align}
w &= \frac{\partial }{\partial x} \tan^{-1} (u) dx + \frac{\partial }{\partial y} \tan^{-1} (u) dy \\
&= -\frac{y}{x^2 + y^2} dx + \frac{x}{x^2 + y^2} dy
\end{align}
$$

#### Note 3.

반대로 $g:\mathbb{R}^2 \rightarrow U$ 로 보내는 함수를 생각해 보자.
그리고 이에 의해 pullback $g^* d\theta$ 에 대한 것을 생각해 보자.

이러한 함수의 가장 일반적인 형태는 **Note 2** 에서 다룬 $\theta =\tan^{-1} (\frac{y}{x})$ 이다. 이것을 Example 처럼 해보자. (즉, $w$를 유도 하는 것)

### Proposition 4
Let $f : \mathbb{R}^n \rightarrow \mathbb{R}^m$ be a differential map. Then 

1. $f^* (w \wedge \varphi) = (f^* w) \wedge (f^* \varphi)$
	- where $w$ and $\varphi$ any two forms in $\mathbb{R}^m$.

2. $(f \circ g)^* w = g^* (f^* w)$,
	- where $g:\mathbb{R}^p \rightarrow \mathbb{R}^n$ is a differentiable map.

#### Sketch of proof
Only for 2. Let $w = \sum_I a_I dy_I$ 

$$
\begin{align}
(f \circ g)^* w &= \sum_{I} a_I ((f \circ g)_1, \cdots, (f \circ g)_m )d( f \circ g)_I \\
&= \sum_{I} a_I (f_1 (g_1, \cdots , g_n), \cdots, f_m (g_1, \cdots , g_n)  ) df_I(dg_1, \cdots, dg_n) \\
&= g^*(f^* w) 
\end{align}
$$

**Q.E.D**
쉽게 생각하면 $h = (f \circ g) : \mathbb{R}^p \rightarrow \mathbb{R}^n \rightarrow \mathbb{R}^m $  그리고 $w$ is defined on $\mathbb{R}^m$ 따라서 $h^* w : \mathbb{R}^m \rightarrow \mathbb{R}^p$ 단계적으로 생각하면 $\varphi = f^* w : \mathbb{R}^m \rightarrow \mathbb{R}^n$ 그리고 $g^* \varphi : \mathbb{R}^n \rightarrow \mathbb{R}^p$

### Differential of 0-form
Let $g : \mathbb{R}^n \rightarrow \mathbb{R}$ be a 0-form. Then the differential 

$$
dg = \sum_{i=1}^n \frac{\partial g}{\partial x_i} dx_i
$$
is a 1-form.

#### Note
여기에서 이렇게 생각할 수 있다.

$$
d = \sum_{i=1}^n \frac{\partial }{\partial x_i} dx_i
$$

이렇게 생각하면 이후의 Definition 5를 비롯하여 Differential 0-form과 이후의 내용들도 이해하기 편하다. 즉, 편미분항은 계수에, Differential은 Differential의 Wedge Product혹은 Exterior derivative가 정의된다.

### Definition 5
Let $w = \sum a_I dx_I$ be a k-form in $\mathbb{R}^n$. The **exterior differential **  $dw$ of $w$ is defined by

$$
dw = \sum_I da_I \wedge dx_I
$$

- - 즉, differential에 Differential 이 붙는 것이 아니라, 계수에 해당하는 함수에 붙는 다는 것.

### Proposition 5
1. $d(w_q + w_2) = dw_1 + dw_2$ where $w_1$ and $w_2$ are k-forms.
2. $d(w \wedge \varphi) = dw \wedge \varphi + (-1)^k w \wedge d\varphi$ where $w$ is k-form and $\varphi$ is an s-form
3. $d(dw) = d^2 w = 0$
4. $d(f^* w) = f^* (dw)$, where $w$ is a k-form in $\mathbb{R}^m$ and $f : \mathbb{R}^n \rightarrow \mathbb{R}^m$ is a differential map.

#### Proof of 3,4
- For 3

$$
\begin{align}
d(df) &= d\left( \sum_{j=1}^n \frac{\partial f}{\partial x_j} dx_j \right) = \sum_{j=1}^n d \left( \frac{\partial f}{\partial x_j} \right) \wedge dx_j \;\;\;\because \text{by definition 5}\\
&= \sum_{j=1}^n \sum_{i=1}^n \left( \frac{\partial^2 f}{\partial x_i \partial x_j}\right) dx_i \wedge dx_j \;\;\;\because \text{by the definition of differential for 0-form}\\
&= \sum_{i \leq j } \left( \frac{\partial^2 f}{\partial x_i \partial x_j} - \frac{\partial^2 f}{\partial x_j \partial x_i}\right) dx_i \wedge dx_j \;\;\; \because \text{by the Proposition 5 -2} \\
&= 0
\end{align} 
$$

- For 4
Let $g : \mathbb{R}^m \rightarrow \mathbb{R}$ so that $(y_1, \cdots y_m) \in \mathbb{R}^m$. Then

$$
\begin{align}
f^*(dg) &= f^* \left( \sum_i \frac{\partial g}{\partial y_i} dy_i \right) \\
&= \sum_{ij} \frac{\partial g}{\partial y_i} \frac{\partial f}{\partial x_j} dx_j \;\;\; \because f^* dy_i = \sum_j  \frac{\partial f}{\partial x_j} dx_j \\
&= \sum_{j} \frac{\partial (g \circ f)}{\partial x_j} dx_j = d (g \circ f) = d(f^* g)
\end{align}
$$

and Let $\varphi = \sum_I a_I dx_I$ be a k-form. Then

$$
\begin{align}
d(f^* \varphi) &= d(\sum_I f^*(a_I) f^*(dx_I)) \\
&= \sum_I d(f^*(a_I)) \wedge f^*(dx_I) \\
&= \sum_I f^* (da_I) \wedge f^*(dx_I) \;\;\;\because \text{The result of the above equation} \\
&= f^* \left( \sum_I da_I \wedge dx_I \right) = f^* (d\varphi)
\end{align}
$$

#### Note 
다음을 살펴보자

$$
f^* dy_i = \sum_j  \frac{\partial f}{\partial x_j} dx_j
$$

그리고 이것을 살펴보자 (위에 있는 Note)

$$
f^* dy_i (v) = dy_i (df(v)) = d(y_i \circ f)(v) = df_i (v)
$$

좀 더 자세하게 보면

$$
d(y_i \circ f) = \sum_{k=1}^n \frac{\partial(y_i \circ f)}{\partial x_k} dx_k = \sum_{k=1}^n \frac{\partial f_i}{\partial x_k} dx_k = df_i
$$


여기서 주의할 것은 $f : \mathbb{R}^n \rightarrow \mathbb{R}^m$ 
이렇게 생각할 수 있다.

$$
\begin{align}
f^*(dg) &= f^* \left( \sum_i a_i dy_i \right) \;\;\;\; \text{where } a_i = \frac{\partial g}{\partial dy_i} \\
&= \sum_i f^*(a_i) f^* dy_i = \sum_i (a_i \circ f) dy_i (df) = \sum_i (a_i \circ f) df_i \\
&= \sum_i (\frac{\partial g}{\partial y_i} \circ f) \frac{\partial f}{\partial x_i}dx_i = \sum_i \frac{\partial (g \circ f)}{\partial f_i}  \frac{\partial f}{\partial x_i}dx_i \\
&= \sum_i \frac{\partial (g \circ f)}{\partial x_i} dx_i = d(g \circ f) = d(f^* g)
\end{align}
$$


#### Problem- 8
Let $f : \mathbb{R}^n \rightarrow \mathbb{R}^n$ be a differentiabkle map given by

$$
f(x_1, \cdots x_n) = (y_1, \cdots, y_n)
$$

and let $w = dy_1 \wedge \cdots \wedge dy_n$ Show that 

$$
f^* w = \det(df) dx_1 \wedge \cdots \wedge dx_n
$$

#### Solve
Let $df_i = d(y_i \circ f)$

$$
\begin{align}
f^* w &= f^* (dy_1 \wedge \cdots \wedge dy_n) = f^* dy_1 \wedge \cdots \wedge f^* dy_n \\
&= dy_1 (df) \wedge \cdots \wedge dy_n(df) = df_1 \wedge \cdots \wedge df_n \\
&= \sum_{k=1}^n \frac{\partial f_1}{\partial x_k} dx_k \wedge \cdots \wedge \sum_{k=1}^n \frac{\partial f_n}{\partial x_k} dx_k  \;\;\; \cdots (1) \\
&= \det(df) dx_1 \wedge \cdots \wedge dx_n \;\;\; \cdots (2)
\end{align}
$$

(1)에서 (2)의 경우는 수학적 귀납법으로 풀거나. 다른 방법을 모색해보자.



