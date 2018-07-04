---
layout: post
title:  "Riemannian Geometry (Very Essential)"
date:   2018-07-05 14:49:00 +0900
categories:
  - Differential Geometry
tags:
  - Differential Geometry
  - Riemannian Geometry 
  - Affine connection
comments: true
---

* Table of Contents
{:toc}

## Parameterization Curve
Let $\alpha : (-\varepsilon, \varepsilon) \rightarrow \mathbb{R}^n$ be a differentiable curve in $\mathbb{R}^n$ with $\alpha(0) = p$ 에서 다음과 같이 정의된다고 할떄
$$
\alpha(t) = (x_1(t), \cdots, x_n(t)), \; t \in (-\varepsilon, \varepsilon), \;\; (x_1, \cdots, x_n) \in \mathbb{R}^n
$$
에서 $f : \mathbb{R}^n \rightarrow \mathbb{R}$ 에 대하여
$$
\frac{d(f \circ \alpha)}{dt} |_{t=0} = \sum_{i=1}^n \frac{\partial f}{\partial x_i} |_{t=0} \frac{dx_i}{dt} |_{t=0} = (\sum_i x_i'(0) \frac{\partial }{\partial x_i}_{0} ) f
$$
따라서 
$$
\alpha'(0) f = \frac{d(f \circ \alpha)}{dt} |_{t=0}
$$
에서 
$$
\alpha'(0) = \sum_i x_i'(0) \left( \frac{\partial }{\partial x_i} \right)_{0}
$$
그래서 $\left( \frac{\partial }{\partial x_i} \right)_{0}$ 는 **Tangent vector at $p$** of the coordinate curve.
그리고 associated basis 
$$
\left\{ \left( \frac{\partial }{\partial x_1} \right)_{0}, \cdots, \left( \frac{\partial }{\partial x_n} \right)_{0} \right\} \;\;\text{in } T_p M
$$

## Vector Fields 

If $\varphi : M \rightarrow M$ is a **diffeomorphism**, $v \in T_p M$ and $f : M \rightarrow \mathbb{R}$ is a differentiable function in a neighborhood of $\varphi(p)$, we have
$$
(d\varphi(v)f)\varphi(p) = v(f \circ \varphi)(p)
$$

- $df$ 자체는 differential 이고 dual인 vector $\nabla f$로 생각할 수 있으나 
$$
df(v) = \langle \nabla f, v \rangle \in \mathbb{R}
$$
마찬가지로 
- $\varphi : M \rightarrow M$ 에서 $d\varphi$ 자체는 **Matrix**로 볼 수 있다.
$$
d\varphi(v) = d\varphi \cdot v
$$
이므로 ($d\varphi$가 **Matrix** 이므로..) $d\varphi(v) = v' \in T_p M$ 라는 또 다른 Vector가 되므로 
$$
d\varphi(v) f = v'(f) = v' f \in \mathbb{R}
$$
로 정의되어 Scalar 

- Definition의 고찰
$$
vf = \langle df, v \rangle = df(v)
$$
즉, $v f = df(v)$ 는 Inner Product 이므로 연산의 우선 순위가 결정되어 있지 않다. 
	- $v (f \circ \varphi) (p)$ 의 경우는 먼저 $\varphi$ 와 $v$의 연산이 실행되어야 한다. 그러므로 $d\varphi(v)$ 의 Matrix -vector 연산이 이루어지고 이것 $d\varphi(v)$과 $f$와의 연산이 이루어져야 한다. 따라서 $(d\varphi(v)f)\varphi(p)$ 이다.

### Proposition 5.4 (p28)
Let $X, Y$ be a differentiable vector fields on a differentiable manifold $M$, let $p \in M$ , and let $\varphi_t$ be the local flow of $X$ in a neighborhood $U$ of $p$. Then
$$
[X,Y](p) = \lim_{t \rightarrow 0} \frac{1}{t}(Y - d\varphi_t Y)(\varphi_t(p))
$$

### Definition of Differential Forms and Basis
$$
(dx_i)_p (e_j) = \frac{\partial x_i}{\partial x_j} = 
\begin{cases}
0 &  \text{if} \; i \neq j \\
1 &  \text{if} \; i = j
\end{cases}
$$
It means that 
$$
ds(\frac{\partial }{\partial u}) = \frac{\partial s--}{\partial u}
$$
## Covariant Derivative
- 공변 미분은 Differential Form을 의미하며 반변 미분은 Vector 그 자체이다.
- 즉, 공변 미분은 $df$, 반변 미분은 $\nabla f$

Surface : $S \subset \mathbb{R}^3$ , Parameterized curve : $c : I \rightarrow S$, and a Vector field along $c$ tangent to $S$ : $V : I \rightarrow \mathbb{R}^3$  

이때, Vector $\frac{dV}{dt}(t), t \in I$ 는 일반적으로 **Tangent space** $T_{c(t)}S$ 에 존재하지 않는다.
그러므로 $\frac{dV}{dt}(t), t \in I$ 이 **Tangent space** $T_{c(t)}S$ 에 존재하도록 Orthogonal Projection 된 미분이 필요하며 그것이 **Covariant Derivative** $\frac{DV}{dt}$ 이다.

1. Covariant Derivative는 the First fundamental form of $S$에 의존적
2. Covariant Derivative는 속도벡터 $c$의 미분으로서 $S$ 위의 $c$의 가속도
3. 무가속도는 **Geodesic of** $S$, 그리고 **Gaussian Curvature of** $S$는 **Covariant Derivative**로 표현

**Parameterized curve c의 시간에 대한 미분 $\frac{dc}{dt}$ 가 Tangent Space의 Basis이므로 이 Basis로 임의의 Vector Field $V(t) = Y(c(t))$를 미분하는 것 $\nabla_{\frac{dc}{dt}} V$ 가 Covariant Derivation이다.**


#### Definition : Affine Connection $\nabla$
An Affine connection $\nabla$ on a differtential manifold $M$ is a mapping 
$$
\nabla : \mathcal{X}(M) \times \mathcal{X}(M) \rightarrow \mathcal{X}(M)
$$

#### Proposition : The Covariant Derivative
If $V$ is induced by a vector field $Y \in \mathcal{X}(M)$ i.e. $V(t) = Y(C(t))$, then 
$$
\frac{DV}{dt} = \nabla_{\frac{dc}{dt}} Y
$$

#### Remark 1
Choosing a system of coordinates $(x_1, \cdot, x_n)$ about $p$ and writing
$$
X = \sum_i x_i X_i, \;\;\; Y=\sum_j y_j X_j \;\;\;\text{where}\;\; X_i = \frac{\partial}{\partial x_i}
$$
then
$$
\nabla_X Y = \sum_k \left( \sum_{ij} x_i y_j \Gamma_{ij}^k + X(y_k) \right) X_k
$$
#### Remark 1-1
where **Christoffel symbol** $\Gamma_{ij}^k$ is defined as 
$$
\nabla_{X_i}X_j = \sum_k \Gamma_{ij}^k X_k
$$
1. Christoffel symbol은 결국 Tensor 이며 각 Component는 그냥 **Scalar** 값이다.
2. 하단의 $i, j$는 원래 입력 벡터의 Component index, 상단의 $k$는 새로운 벡터의 Component index 
3. 결국 Affine Connection에 의해 만들어지는 새로운 벡터필드에 대한 Parameter 이다.

##### proof
$$
\nabla_X Y = \sum_i x_i \nabla_{X_i} \left( \sum_j y_j X_j \right) = \sum_i x_i \left( \sum_j X_i(y_j) X_j + y_j \nabla_{X_i} X_j\right)
$$
Thus,
$$
\nabla_{X_i}X_j = \sum_k \Gamma_{ij}^k X_k, \;\;\; \sum_i \sum_j x_i X_i(y_j) X_j = \sum_j X(y_j) X_j = \sum_k X(y_k) X_k
$$
$X(y_k)$ 는 결국 $ \langle X, dy_k \rangle \in \mathbb{R}$ 따라서,
$$
\sum_{ij}x_i X_i(y_j)X_j + \sum_{ij}x_i y_j \nabla_{X_i} X_j = \sum_k \left( X(y_k) + \sum_{ij} x_i y_j \Gamma_{ij}^k  \right)X_k
$$
** Q.E.D **

#### Total Covariant (Essential)
Let 
$$
V = \sum_j v^j X_j , \;\; v^j = v^j(t), \;\; X_j = X_j(c(t))
$$
Then
$$
\frac{DV}{dt} = \frac{D}{dt} \left( \sum_j v^j X_j \right) = \sum_j \frac{dv^j}{dt} X_j + \sum_j v^j \frac{DX_j}{dt}
$$
이떄 
$$
\frac{DX_j}{dt} = \nabla_{\frac{dc}{dt}}X_j, \;\;\; \frac{dc}{dt} = \sum_i \frac{dx_i}{dt}X_i 
$$
이므로 
$$
\frac{DX_j}{dt}= \nabla_{\frac{dc}{dt}}X_j= \nabla_{\sum_i \frac{dx_i}{dt}X_i } X_j = \sum_i \frac{dx_i}{dt} \nabla_{X_i}X_j = \sum_i \frac{dx_i}{dt} \sum_k \Gamma_{ij}^k X_k
$$
Index 정리를 하면
$$
\begin{align}
\frac{DV}{dt} &= \sum_j \frac{dv^j}{dt} X_j + \sum_j v^j \sum_i \frac{dx_i}{dt} \sum_k \Gamma_{ij}^k X_k \\
&= \sum_j \frac{dv^j}{dt} X_j + \sum_{i,j} v^j \frac{dx_i}{dt} \sum_k \Gamma_{ij}^k X_k \\
&= \sum_k \left( \frac{dv^k}{dt} + \sum_{i,j} v^j \frac{dx_i}{dt} \Gamma_{ij}^k \right)X_k
\end{align}
$$
특히 **Parallel Transportation**이 되기 위해서는 위 Covariant Derivative가 0이 되어야 하므로 
$$
\frac{dv^k}{dt} + \sum_{i,j} v^j \frac{dx_i}{dt} \Gamma_{ij}^k = 0
$$

## Riemannian Connection
### Definition : Symmetric Connection
An affine connection  on a smooth manifold $M$ is said to be symmetric when
$$
\nabla_X Y - \nabla_Y X = [X, Y], \;\; X, Y \in \mathcal{X}(M)
$$
If $X = X_i, Y= X_j, X_k = \frac{\partial}{\partial x_i}$ 이면
$$
0 = [X_i, X_j] = \nabla_{X_i} X_j - \nabla_{X_j} X_i = \sum_k (\Gamma_{ij}^k - \Gamma_{ji}^k) X_k
$$
에서 $\Gamma_{ij}^k = \Gamma_{ji}^k$ 이므로 Symmetric 
또한 Lie Bracket이 이렇게 정의된다.

### Levy-Civita Theorem
Given a Riemannian manifold $M$, there exists a unique affine connection $\nabla$ satisfying the conditions :

1. is symmetric
2. is compatible with the Riemannian metric

#### Remark 
$$
\begin{align}
X \langle Y, Z \rangle &= \langle \nabla_X Y, Z \rangle + \langle Y, \nabla_X Z\rangle \;\;\;\text{....1} \\
Y \langle Z, X \rangle &= \langle \nabla_Y Z, X \rangle + \langle Z, \nabla_Y X\rangle \;\;\;\text{....2} \\
Z \langle X, Y \rangle &= \langle \nabla_Z X, Y \rangle + \langle X, \nabla_Z Y\rangle \;\;\;\text{....3} 
\end{align}
$$
1 + 2 - 3 (Very Important)
$$
\begin{align}
X \langle Y, Z \rangle + Y \langle Z, X \rangle - Z \langle X, Y \rangle &= \langle \nabla_X Y, X \rangle + \langle Y, \nabla_X Z \rangle \\
&+ \langle \nabla_Y Z, X \rangle + \langle Z, \nabla_Y X \rangle - \langle \nabla_Z X, Y \rangle - \langle X, \nabla_Z Y \rangle \\
&= \langle Y, \nabla_X Z \rangle - \langle Y, \nabla_Z X \rangle + \langle X, \nabla_Y Z \rangle - \langle X, \nabla_Z Y \rangle \\
&+ \langle Z, \nabla_X Y \rangle - \langle Z, \nabla_Y X \rangle + 2 \langle Z, \nabla_Y X \rangle \\
&=  \langle [X, Z], Y \rangle + \langle [Y,Z], X \rangle + \langle [X, Y], Z \rangle + 2 \langle Z, \nabla_Y X \rangle
\end{align}
$$
$$
\langle Z, \nabla_Y X \rangle = \frac{1}{2} \left( X \langle Y, Z \rangle + Y \langle Z, X \rangle - Z \langle X, Y  \rangle - \langle [X, Z], Y \rangle - \langle [Y,Z], X \rangle - \langle [X, Y], Z \rangle\right) ...\text{4}
$$

Assume that $X = \frac{\partial}{\partial x_i}, Y = \frac{\partial}{\partial x_j}, Z = \frac{\partial}{\partial x_k}$ then, $[X, Y]=[Y,Z]=[Z, X] = 0$  
Symmetry and 
$$
\langle \nabla_Y X, Z \rangle = \langle \sum_l \Gamma_{ij}^l X_l, X_k \rangle= \sum_l \Gamma_{ij}^l \langle X_l, X_k \rangle = \sum_l \Gamma_{ij}^l g_{lk}
$$
Thus, The equation 4 is 
$$
\sum_l \Gamma_{ij}^l g_{lk} = \frac{1}{2} \left( \frac{\partial}{\partial x_i} g_{jk} + \frac{\partial}{\partial x_j} g_{ki} - \frac{\partial}{\partial x_k} g_{ij} \right)
$$
이때, the matrix $(g_{km})$ admits an inverse $(g^{km})$ 이면.
$$
\sum_k \sum_l \Gamma_{ij}^l g_{lk} g^{km} = \frac{1}{2} \sum_k \left( \frac{\partial}{\partial x_i} g_{jk} + \frac{\partial}{\partial x_j} g_{ki} - \frac{\partial}{\partial x_k} g_{ij} \right) g^{km}
$$
$l = m $ 일때만 1 이고 나머지 경우는 0 이고 좌항의 $k$와 $m$이 맞추어져야 하므로 즉, $g_{mk} = g^{km}$ 의 경우 1이고 나머지는 0이된다. (대각성분만 남게 된다.) 그러므로 
$$
\Gamma_{ij}^m = \frac{1}{2} \sum_k \left( \frac{\partial}{\partial x_i} g_{jk} + \frac{\partial}{\partial x_j} g_{ki} - \frac{\partial}{\partial x_k} g_{ij} \right) g^{km}
$$

### Definition of Christoffel Symbol
$$
\Gamma_{ij}^m = \frac{1}{2} \sum_k \left( \frac{\partial}{\partial x_i} g_{jk} + \frac{\partial}{\partial x_j} g_{ki} - \frac{\partial}{\partial x_k} g_{ij} \right) g^{km}
$$
하지만, 실제 Christoffel 기호는 위 식으로 구할 수 없으며..(단지 정의일 뿐) 및에서와 같이 Reimannian Metric 과 Affine Connection을 사용하여야 정상적으로 풀 수 있다.

#### Exercise (How to get the christoffel symbol)
Consider the upper half-plane 
$$
\mathbb{R}_{+}^2 = \{ (x,y) \in \mathbb{R}^2; y > 0 \}
$$
with the metric given by $g_{11} = g_{22} = \frac{1}{y^2}, g_{12} = 0$ 
일때, $\Gamma_{11}^1 = \Gamma_{12}^2 = \Gamma_{22}^1 = 0, \Gamma_{11}^2 = \frac{1}{y}, \Gamma_{12}^1 = \Gamma_{22}^2 = -\frac{1}{y}$ 임을 보여라. (1 이 $x$ , 2가 $y$를 의미한다.)
##### Solve

$$
\begin{align}
0 &= \nabla_{X_1} g_{11} = \nabla_{X_1} \langle X_1, X_1 \rangle = 2\nabla_{X_1} X_1 \cdot X_1 = 2(\Gamma_{11}^1 X_1 \cdot X_1 + \Gamma_{11}^2 X_2 \cdot X_1) \;\;\;X_2 \cdot X_1 = 0 , \;\;\Gamma_{11}^1 = 0 \\
0 &= \nabla_{X_1} g_{12} = \nabla_{X_1} \langle X_1, X_2 \rangle = \nabla_{X_1} X_1 \cdot X_2 + \nabla_{X_1} X_2 \cdot X_1 \\
&= \Gamma_{11}^1 X_1 \cdot X_2 + \Gamma_{11}^2 X_2 \cdot X_2 + \Gamma_{12}^1 X_1 \cdot X_1 + \Gamma_{12}^2 X_2 \cdot X_1 = \Gamma_{11}^2 X_2 \cdot X_2 + \Gamma_{12}^1 X_1 \cdot X_1 = \Gamma_{11}^2 + \Gamma_{12}^1 \\
0 &= \nabla_{X_1} g_{22} = \nabla_{X_1} \langle X_2, X_2 \rangle = 2\nabla_{X_1} X_2 \cdot X_2 = 2(\Gamma_{12}^1 X_1 \cdot X_2 + \Gamma_{12}^2 X_2 \cdot X_2) \;\;\because \Gamma_{12}^2 = 0 \\
0 &= \nabla_{X_2} g_{12} =\nabla_{X_2} \langle X_1 , X_2 \rangle = \nabla_{X_2} X_1 \cdot X_2 + \nabla_{X_2} X_2 \cdot X_1 \\
&= \Gamma_{21}^1 X_1 \cdot X_2 + \Gamma_{21}^2 X_2 \cdot X_2 + \Gamma_{22}^1 X_1 \cdot X_1 + \Gamma_{22}^2 X_2 \cdot X_1 = \Gamma_{21}^2 + \Gamma_{22}^1  \because \Gamma_{21}^2 = \Gamma_{12}^2 = 0, \;\; \Gamma_{22}^1 = 0 \\
\nabla_{X_2} g_{11}&= \frac{\partial}{\partial y}\left( \frac{1}{y^2}\right) = -2 \frac{1}{y^3} = 2 \cdot \nabla_{X_2} X_1 \cdot X_1 = 2 \cdot \left( \Gamma_{21}^1 X_1 \cdot X_1 + \Gamma_{21}^2 X_2 \cdot X_1\right) \\
&= 2 \cdot \Gamma_{21}^1 X_1 \cdot X_1 = 2 \cdot \Gamma_{21}^1 \langle X_1, X_1 \rangle = 2 \cdot \Gamma_{21}^1 g_{11} = 2 \cdot \Gamma_{21}^1 \frac{1}{y^2} \;\;\therefore \Gamma_{21}^1 = \Gamma_{12}^1 = -\frac{1}{y} \\
\nabla_{X_2} g_{22}&= \frac{\partial}{\partial y}\left( \frac{1}{y^2}\right) = -2 \frac{1}{y^3} = 2 \cdot \nabla_{X_2} X_2 \cdot X_2 = 2 \cdot \left( \Gamma_{22}^1 X_1 \cdot X_2 + \Gamma_{22}^2 X_2 \cdot X_2\right) \\
&= 2 \cdot \Gamma_{22}^2 X_2 \cdot X_2 = 2 \cdot \Gamma_{22}^2 \langle X_2, X_2 \rangle = 2 \cdot \Gamma_{22}^2 g_{22} = 2 \cdot \Gamma_{22}^2 \frac{1}{y^2} \;\;\therefore \Gamma_{22}^2 = - \frac{1}{y} \\
&\because \;\;\Gamma_{11}^2 + \Gamma_{12}^1 = 0, \;\;\Gamma_{11}^2 = -\Gamma_{12}^1 = \frac{1}{y}
\end{align}
$$

**위 방법은 Riemmanian Connection $\Gamma_{ij}^k$를 Reiemannian Metric $g_{jk}$ 로 부터 구하는 일반적인 방법이다.**

