---
layout: post
title:  "Solution of Fokker Plank Equation"
date:   2019-07-01 01:45:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
  - Geometrical SDE
comments: true
---

* Table of Contents
{:toc}


## Stationary Solutions for Homogeneous Fokker-Plank Equation

If FP equation is given by 

$$
\frac{\partial p_s}{\partial t}(x) = -\frac{\partial}{\partial x} \left( A(x)p_s(x) \right) + \frac{1}{2} \frac{\partial^2}{\partial x^2} \left( B(x)p_s(x) \right)
$$

, then a homogeneous solutions of FP is same to the following:

$$
\frac{d}{d x} \left( A(x)p_s(x) \right) - \frac{1}{2} \frac{d^2}{d x^2} \left( B(x)p_s(x) \right) = 0
$$

It means that

$$
A(x)p_s(x) - \frac{1}{2} \frac{d}{d x} \left( B(x)p_s(x) \right) = 0.
$$

It is a simple oridinary differential equation. For convenience, we set a function $C(x)$ such that $C(x) = B(x)p_s(x)$, so that we evaluate the equation,

$$
\begin{aligned}
A(x)p_s(x) &= \frac{1}{2} \frac{d}{d x} \left( B(x)p_s(x) \right) \\
2 \cdot C(x)\frac{A(x)}{B(x)} &= \frac{d}{d x} C(x) \\
2 \cdot \frac{A(x)}{B(x)} dx &= \frac{1}{C(x)} dC(x) \\
C_0 \exp \left( 2 \int_0^x  \frac{A(\bar{x})}{B(\bar{x})} d\bar{x} \right) &= C(x) \\
p_s(x) &= \frac{C_0}{B(x)} \exp \left( 2 \int_0^x  \frac{A(\bar{x})}{B(\bar{x})} d\bar{x} \right)
\end{aligned}
\label{eq01:ST}
\tag{S1}
$$

where $C_0$ is a **normaliztion constant** such that $\int_0^b dx p_s(x) = 1$, thus

$$
\begin{aligned}
1 = \int_R p_s(x) dx &= \int_R \frac{C_0}{B(x)} \exp \left( 2 \int_0^x  \frac{A(\bar{x})}{B(\bar{x})} d\bar{x} \right) dx\\
&= C_0 \int_R \frac{1}{B(x)} \exp \left( 2 \int_0^x  \frac{A(\bar{x})}{B(\bar{x})} d\bar{x} \right) dx \\
\Rightarrow C_0 &= \frac{1}{\int_R \frac{1}{B(x)} \exp \left( 2 \int_0^x  \frac{A(\bar{x})}{B(\bar{x})} d\bar{x} \right) dx}
\end{aligned}
$$

### Potential dynamics

The foward equation 

$$
\frac{\partial p}{\partial t}(z, t) = - \sum_{i}\frac{\partial p}{\partial z_i} A_i(z, t)p(z, t) + \frac{1}{2} \sum_{i,j} \frac{\partial^2}{\partial z_i \partial z_j} B_{ij} (z, t) p(z, t)
\label{eq02:PD}
\tag{S2}
$$

is equivalent to 

$$
\frac{\partial p}{\partial t}(z, t) + \sum_{i} \frac{\partial}{\partial z_i} J_i(z, t) = 0
\label{eq03:PD}
\tag{S3}
$$

where we define the probablity current

$$
J_i (z, t) = A_i (z, t) p(z, t) - \frac{1}{2} \sum_j \frac{\partial }{\partial z_j} B_{ij}(z, t)p(z, t).
$$

Consider some REgion $R$ with a boundatry $S$ and define

$$
P(R, t) = \int_R p(z, t) dz = \int_R dz p(z, t) 
$$

then $\eqref{eq03:PD}$ is equivalent to 

$$
\frac{\partial P(R, t)}{\partial t} = - \int_S n \cdot J(z,t) dS = = - \int_S dS n \cdot J(z,t) 
\label{eq04:PD}
\tag{S4}
$$

where $n$ is the outward pointning normal to $S$.

Therefore, $\eqref{eq04:PD}$ indicates that **the total loss of probablity** is given by **the surface integral of $J$ over the boundary of $R$**.

- 그러므로 Homogeneous Fokker Plank 방정식의 경우  $\eqref{eq02:PD}$ 에서 

$$
\frac{dJ}{dz}(z, t) = 0
$$

인 경우이며, 이 경우는 정통적인 1-st order Necessity Condition이 된다.

### Stationary Solution of Gradient Descent

If the learning equation based on a stochastic gradient rule is given by

$$
dX_t = - \nabla U(X_t) dt + \sqrt{T(t)} dW_t
\label{eq05:GD}
\tag{S5}
$$

, then the Fokker-Plank equation of $\eqref{eq05:GD}$ is 

$$
\frac{\partial p}{\partial t}(x, t) = \frac{\partial}{\partial x} \left( \nabla U(x) p(x, t) \right) + \frac{1}{2} T(t) \frac{\partial^2 p}{\partial x^2}(x, t)
\label{eq06:GD}
\tag{S6}
$$

, and the stationary solution of the $\eqref{eq06:GD}$ is 

$$
\begin{aligned}
p(x, t)
&= \frac{C_0}{B(x)} \exp \left( 2 \int_0^x  \frac{A(\bar{x})}{B(\bar{x})} d\bar{x} \right) \\
&= \frac{C_0}{T(t)} \exp \left( 2 \int_0^x  \frac{-\nabla U (\bar{x})}{T(t)} d\bar{x} \right) \\
&= \frac{C_0}{T(t)} \exp \left( -2 \frac{1}{T(t)} \int_0^x \nabla U (\bar{x})d\bar{x} \right) \\
&= \frac{C_0}{T(t)} \exp \left( -2 \frac{U (x)}{T(t)}\right) 
\end{aligned}
\label{eq07:GD}
\tag{S7}
$$

By definition, $C_0$ is a normalization parameter such that 

$$
\begin{aligned}
C_0 &= \frac{1}{\int_R \frac{1}{B(x)} \exp \left( 2 \int_0^x  \frac{A(\bar{x})}{B(\bar{x})} d\bar{x} \right) dx} \\
&= \frac{1}{\frac{1}{T(t)}\int_R \exp \left( -2 \frac{U (x)}{T(t)}\right) dx} \\
&= \frac{T(t)}{\int_R \exp \left( -2 \frac{U (x)}{T(t)}\right) dx}. 
\end{aligned}
$$

Therefore, the stationary solution of gradient descent is 

$$
p(x, t) = \frac{1}{Z(x)} \exp \left( -2 \frac{U (x)}{T(t)}\right) 
$$

where $Z(x) = \int_R \exp \left( -2 \frac{U (x)}{T(t)}\right) dx$.

The stationary solution of the Fokker Plank equation to  the stochastic gradient rule $\eqref{eq05:GD}$ is **Gibb's distribution** or **Boltzmann distribution**.

