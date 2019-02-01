Constrained Optimization
===========

## Lagrangian Method


### Idea of Equality Contrained 
다음과 같은 최적화 문제가 있다고 하자. $x = (x_1, x_2, x_3) \in \mathbb{R}^n$ 에 대하여 다음과 같이 등식 제한 조건이 있는 최적화 문제가 주어졌다.
$$
\begin{align}
Object : &\min_{x_1, x_2, x_3} f(x_1, x_2, x_3) \\ 
Subject: &h_1(x_1, x_2, x_3) = 0, \;\; h_2(x_1, x_2, x_3) = 0
\end{align}
$$

이때 제한 조건에 의해 최적점이 위치할 곳은 $\mathbb{R}^3$ 상의 어떤 **Curve** 이다. 
이렇게 제한 조건에 의해 최적점이 위치할 수 있는 영역을 **Feasible Region $S$** 라고 한다.
이 문제를 풀기 위해 다음과 같이 변수를 변경해 문제를 $x_1$ 에 대한 최적화 문제로 바꾸어 보자
$$
x_2 = u(x_1), \;\;\; x_2 = v(x_1) \\
\min_{x_1} f(x_1, u(x_1), v(x_1))
$$
이 경우, $f(x)$는 $x^*$에 대하여 $\nabla f(x^*) = 0$ 이므로
$$
\frac{\partial f}{\partial x_1} + \frac{\partial f}{\partial u} \frac{\partial u}{\partial x_1} + \frac{\partial f}{\partial v} \frac{\partial v}{\partial x_1} = 0 
$$
그리고 $h_i(x) = 0, i=1,2$ 이므로 $\nabla h(x) = 0$ 이므로
$$
\frac{\partial h_i}{\partial x_1} + \frac{\partial h_i}{\partial x_1} \frac{\partial u}{\partial x_1} + \frac{\partial h_i}{\partial v} \frac{\partial v}{\partial x_1} = 0 
$$
따라서, Matrix $A = [\nabla f(x^*), \nabla h_1 (x^*), \nabla h_2 (x^*)] \in \mathbb{R}^{3 \times 3}$ 이라 놓으면
$$
A
\begin{bmatrix}
1 \\
\frac{du}{dx_1} \\
\frac{dv}{dx_1} 
\end{bmatrix}
= 0
$$

이다.
이것이 성립하려면 $[1, \frac{du}{dx_1}, \frac{dv}{dx_1}]^T \neq 0$ 이므로 
**A의 Determinent가 0이 되어야 한다.** 다시말해, **A가 Linearly Dependent 해야 한다.** 즉,
$$
\alpha \nabla f(x^*) + \beta \nabla h_1(x^*) + \gamma \nabla h_2(x^*) = 0
$$

이를 $\alpha$에 대하여 나누게 되면 다음과 같이 쓸 수 있다.
$$
\nabla f(x^*) + \lambda_1 \nabla h_1(x^*) + \lambda_2 \nabla h_2(x^*) = 0
$$
이때, $\lambda_1, \lambda_2$를 Largrangian Multiplier라고 한다. 
위 방정식의 조건은 $x^*$가 Constrained Condition하에서 $f(x)$의 minimum point가 되기 위한 **Necessary Condition** 이다.
따라서, 등식 제한 조건을 가진 최적화 문제는 다음으로 정의되는 **Largrangian** 의 **Critical Point를 찾는 문제이다.**

$$
\phi(x) = f(x) + \lambda_1 h_1(x) + \lambda_2 h_2(x)
\tag{1}
$$

이렇게 Formulation 된 다음 과정을 통해 $x^*$를 찾게 된다.
- $x^*$를 $\lambda_1, \lambda_2$로 나타낸다. such that $x^*(\lambda_1, \lambda_2)$ 
- 이렇게 하면, $x^*(\lambda_1, \lambda_2)$는 Minimum point of the problem.

이를 임의의 $n$ 차원으로 확대해 보자.

### Geometrical Representation

방정식 (1)을 기하하적으로 생각해보자. 방정식 (1)은 결국 $\nabla f(x^*) = - (\lambda_1 \nabla h_1(x^*) + \lambda_2 \nabla h_2(x^*))$ 에서 $\nabla f(x^*)$ 는 $\nabla h_i(x^*)$의 1차 결합임을 알 수 있다. 그러므로 **$\nabla f(x^*)$는 $h_i(x^*)$가 이루는 Tangent Space에 Normal인 Spce에 존재**하게 된다.

![Fig_10_01](http://jnwhome.iptime.org/img/Nonlinear_Optimization/10_01.png "Title" "width:50%;height:50%")

### Proposition 1.
Let $f(\cdot)$ have a local minimum point $x^*$ subject to the equality constaints $h_j(x) = 0, j=1, \cdots , m$ (**등식제한조건**).
Let $f$ and $h_j, j=1, \cdots , m$ be continuously differentiablein an open set containg $x^*$ and 
let $\nabla h_j(x^*), j=1, \cdots, m$ be linearly independent. 
Then, $\langle \nabla f(x^*), z \rangle = 0$ for all $z$ satisfying
$$
G(x^*) z = 0
$$
where 
$$
G(x) = [\nabla h_1(x), \cdots, \nabla h_m(x)]^T
$$

#### proof
위 명제가 성립하지 않는다고 하자, 다시말해 $G(x^*) z = 0$ 이지만, $\langle \nabla f(x^*), z \rangle \neq 0$ 라고 하자.
Then, there exist a mapping from $\mathbb{R}^n$ to $\mathbb{R}^{m+1}$ such that
$$
x \rightarrow 
\begin{bmatrix}
\nabla f(x)^T \\
G(x)
\end{bmatrix}
$$
associated the mapping
$$
x \rightarrow 
\begin{bmatrix}
f(x) \\
g(x)
\end{bmatrix}
$$
is "onto" $\mathbb{R}^{m+1}$ since the mapping $x \rightarrow G(x)$ is onto $\mathbb{R}^m$.

By the inverse theorem, we know that for any $\varepsilon > 0$, there exists a $\delta > 0$ and $x$ in the neighborhood of $x^*$ with $\| x - x^* \| < \varepsilon$ such that

$$
x \rightarrow 
\begin{bmatrix}
f(x^*) - \delta \\
0
\end{bmatrix}
$$
(g(x)가 모두 0인 까닭은 $h_j(x) = 0, j=1, \cdots , m$ 이기 때문 )

**This contradicts the assumption that $x^*$ is a local minimum.**
따라서 증명 끝.

### Proposition 2 : Largrange Multiplier Theorem.
If a continuously differentiable function $f$ has a local minimum subject to the constrained $h(x) = 0$ at $x^*$ such that the rank $G(x^*) = m$, then there exists $\lambda \in \mathbb{R}^m$ such that the Largrangian
$$
\phi(x, \lambda) = f(x) + \langle \lambda, h(x) \rangle 
$$
has $x^*$ as its critical point, that is
$$
\nabla f(x^*) + G^T(x^*) \lambda = 0
$$

#### proof
Propositon 1에서 $\langle \nabla f(x^*), z \rangle = 0$ for all $z$ satisfying $G(x^*) z = 0, \;\; \forall z$ 이기 때문에 **$\nabla f(x)$ 는 $G(x^*)$의 Null space에 대하여 Orthogonal** 하다. ($z$는 $G(x^*) z = 0$ 이므로 $G(x^*)$의 Null space. 그런데 $\langle \nabla f(x^*), z \rangle = 0$ 이므로) 

즉,
$$
\mathcal{N}[G(x^*)]^{\perp} = \mathcal{R}[G^T(x^*)]
$$
이기 떄문에 $\nabla f(x^*) \in \mathcal{R}[G^T(x^*)]$.

Thus, there exists $-\lambda \in \mathbb{R}^m$ such that
$$
\nabla f(x^*) = -G^T(x^*) \lambda
$$
($\nabla f(x^*)$ 와 $G^T(x^*)$ 가 같은 공간 상에 있으므로 1차 변환상, 두 값이 같게 만들어 주는 $-\lambda$ 가 존재한다.)

so that
$$
\nabla f(x^*) + G^T(x^*) \lambda = 0
$$

이를 정리하면 다음과 같다. 제한 조건이 모두 $l$개 있다고 가정하면, i.e. $h_i(x) = 0, i=1, \cdots, l$

$$
\nabla f(x^*) + \sum_{i=1}^l \lambda_i \nabla h_i(x^*) = 0
$$
따라서 Largrangian을 다음과 같이 정의하면 
$$
\phi(x) = f(x) + \sum_{i=1}^l \lambda_i h_i(x)
$$
여기에 대하여
$$
\begin{align}
0 &= \phi(x^*) \\
&= \nabla f(x^*) + \sum_{i=1}^l \lambda_i \nabla h_i(x^*)
\end{align}
$$

그리고 등식 제한 조건에서 
$$
\sum_{i=1}^l \lambda_i \nabla h_i(x^*) = 0
$$

이므로 $f(x^*) = \phi(x^*) = 0$ 이 필요충분 조건으로 만족된다.

#### Example
$$
\begin{align}
\text{min        }   &f(x) = x_1 \cdot x_2 + 14 \\
\text{Subject to } : &x_1^2 + x_2^2 = 18
\end{align}
$$
![Fig_10_01](http://jnwhome.iptime.org/img/Nonlinear_Optimization/10_02.png "Title" "width:25%;height:25%")

Let $h(x) = x_1^2 + x_2^2 - 18 = 0$ Then, $\nabla f(x) = (x_2, x_1)^T$ , $\nabla h(x) = (2x_1, 2x_2)^T$  
Let the largrabgian as $\phi(x) = f(x) + \lambda \cdot g(x)$  then,
$$
0 = \nabla \phi(x) = \nabla f(x) + \lambda \nabla h(x) \Rightarrow \nabla f(x) = -\lambda \nabla h(x) \\
\Rightarrow
\begin{bmatrix}
x_2 \\
x_1 
\end{bmatrix}
= 2 \cdot \lambda \cdot
\begin{bmatrix}
x_1 \\
x_2 
\end{bmatrix} \\
x_2 = 2 \cdot \lambda x_1, \;\; x_1 = 2 \cdot \lambda x_2  \Rightarrow \lambda = \frac{x_2}{2x_1}, \;\; \lambda = \frac{x_1}{2x_2} \\
\Rightarrow \frac{x_2}{2x_1} = \frac{x_1}{2x_2} \Rightarrow x_1^2 = x_2^2
$$
그러므로 $h(x) = x_1^2 + x_2^2 - 18 = 0$ 에서 $2x_1^2 = 18$, $x_1 = \pm 3, y_1 = \pm 3$ 
이를 $f(x)$ 에 대입해보면, $f(3,3) = f(-3,-3) = 23$, $f(3, -3) = f(-3,3) = 5$ 
Minimum 값은 5 이다.

## Inequality Subject : 부등식 제한조건
실제 최적화 문제에서 많이 나타나는 형태는 등식 제한 조건 보다는 부등식 제한 조건의 형태이다.
부등식 제한 조건에 대한 이론을 살펴보기 위하여 먼저, 흔하게 나타나는 형태인 Linear 방정식 형태의 제한 조건에 대하여 알아본다.

- 사실, 부등식 제한 조건의 경우, 제한 조건이 만든 어떤 영역내에 minimizer가 존재하면 제한 조건의 의미는 없다. 그냥 Unconstrained Optimization
- 부등식 제한 조건이 의미가 있는 것은 결국 위의 등식 제한 조건 처럼 제한 조건의 극한 값에서 Minimizer가 존재하기 떄문이다. 

#### Farkas Lemma 
(증명없이 사용한다.)
Let $b \in \mathbb{R}^n $, and an $m \times n$ matrix $A$ be given.
Suppose there exists a nonzero $x \in \mathbb{R}^n$ such that $Ax \geq 0$.
Then $\langle b, x \rangle \geq 0$ for all x satisfying $Ax \geq 0$ if and only if
$$
b = A^T \lambda 
$$
for some $\lambda \geq 0$.

** 다음과 같은 의미 **
Matrix $A^T = [a^1, a^2, \cdots, a^m ]$ 에 대하여, Farkas Lemma는 다음을 필요 충분 조건으로 만족함을 의미한다. 
$$
\langle a^i, x \rangle \geq 0, \;\;\; 1 \leq i \leq m
$$
to implies that 
$$
\langle b. x \rangle \geq 0
$$
이를 그림으로 나타내면 다음과 같다. 

![Fig_10_03](http://jnwhome.iptime.org/img/Nonlinear_Optimization/10_03.jpg "Title" "width:50%;height:50%")

그림에서 벡터 $x$와 $a^i$ 는 $\langle a^i , x \rangle \geq 0$ 이다. 그런데, 벡터 $b$도 $\langle b, x \rangle \geq 0$ 이면 벡터 $a^i$ 로 이루어진 다각형 내부에 벡터 $b$를 위치 시킬 수 있다는 의미이다. 

이렇게 되면, 어떠한 부등식 제한 조건 내에 최적화 시키고자 하는 어떤 함수를 위치 시킬 수 있다는 의미이다.


### Linear inequality
$$
\min f(x), \;\;\;\; \text{subject to } g_i(x) = \langle n_i , x \rangle + b_i \leq 0, \;\;\; 1 \leq i \leq m
$$

따라서 부등식 제한 조건식은 Feasible Region $S$를 둘러싼 다면체를 구성한다고 가정하자.
벡터 $n_i$는 부등식 제한조건에서 $g_i (x) = 0$ 방정식에 대하여 Normal인 벡터로서 Feasbile Region방향으로의 벡터이다.
$x^*$를 제한조건하에서의 최적점 (여기서는 최소점)이라고 가정하자. 
이때,Active constrainetdml index 집합을 다음과 같이 정의하자.
$$
I = \{ i: g_i (x^*) = 0  \}
$$
만일, 집합 $I$가 공집합이면 이는 Unconstrained Optimization 문제이다. 
다음 그림은 $n=2$, $m=3$ and $I = {1, 3}$ 인 경우이다. 

![Fig_10_04](http://jnwhome.iptime.org/img/Nonlinear_Optimization/10_05.png "Title" "width:50%;height:50%")

위 그림에서 $x \in S$를 하나 잡자, 그러면 $x - x^*$는 $x^*$ 에서 $S$ 안쪽으로 들어가는 벡터가 된다. 이를 **Entering Vector** 라고 하자.
그러면
$$
\langle n_i, x - x^* \rangle \geq 0, \;\;\;\text{or}\;\;\; \langle \nabla g_i(x^*), x- x^* \rangle \leq 0\;\;\; \forall i \in I, \; x \in S
$$

Since $n_i = - \nabla g_i (x^*)$ 
그런데 $x^*$는 $f(x)$의 minimizer이므로 
$$
\langle \nabla f(x^*), x - x^* \rangle \geq 0 
$$

Farkas Lemma에 의해 $\langle n_i, x - x^* \rangle \geq 0$ 이므로 $n_i$의 선형 결합으로 이루어진 벡터 $b = \sum_{i \in I} \lambda_i n_i$ 가 존재한다는 것이다. 그러므로 $\langle \nabla f(x^*), x - x^* \rangle \geq 0$  에서 $\nabla f(x^*)$ 와 $b = \sum_{i \in I} \lambda_i n_i$ 는 동등하다고 볼 수 있다. 따라서,
$$
\nabla f(x^* = \sum_{i \in I} \lambda_i n_i = - \sum_{i \in I} \lambda_i \nabla g_i (x^*) \;\;\;\forall \lambda \geq 0
$$
그런데, $f(x^*) = 0$ 이어야 하므로 만일, $j \notin I$ 이면 $\lambda_j = 0$ 그리고 $j \in I $에 대해서는 $g_j(x^*) = 0$ 이어야 한다. 그러므로 
$$
\sum_{j=1}^n \lambda_j g_j(x^*) = 0
$$

따라서 선형 부등식 제한 조건이 있는 경우 Object function은 다음과 같다. 
$$
\phi(x) = f(x) + \sum_{i=1}^m \lambda_i g_i (x)
$$
그리고 minimizer $x^*$는 다음을 만족한다.
$$
\nabla \phi(x^*) = \nabla f(x^*) + \sum_{i=1}^m \lambda_i \nabla g_i(x^*) = 0 \\
\sum_{i=1}^m \lambda_i g_i(x^*) = 0
$$


### Khun-Tucker Condition : Nonlinear Inequality Constraints 
제한 조건이 비선형인 경우를 생각해 보자.
제한 조건이 비선형일 경우에, 비선형 제한 조건의 Gradient는 선형 제한 조건의 경우와 같이 제한 조건 함수의 Tangent Space에 대하여 Normal이다 그러므로 사실상, 선형 제한 조건의 경우와 같은 문제가 된다.

![Fig_10_06](http://jnwhome.iptime.org/img/Nonlinear_Optimization/10_06.png "Title" "width:50%;height:50%")

#### Fritz-John Theorem
Let $f, g, 1 \leq i \leq m$ have continuous partial derivatives in some open set in $\mathbb{R}^n$ containing $x^*$ . 
If $x^*$ is a constrained minimum point of $f(x)$ subject to $g_i(x) \leq 0, \; 1 \leq i \leq m$, then there exists $\lambda_i, i=0, 1, \cdots m$ not all zero satisfying

$$
\lambda_0 \nabla f(x^*) + \sum_{i=1} \lambda_i \nabla g_i(x^*) = 0 \\
\sum_{i=1}^m \lambda_i g_i (x^*) = 0 \\
\lambda_i \geq 0, \;\;\; 0 \leq i \leq m, \;\;\; \lambda_0 \ne 0
$$

여기서 $\lambda_i$에 대하여 $\lambda_i / \lambda_0$ 를 수행하면 $\lambda_0 = 1$이 되어 위의 linear inequality constraints 문제의 해법과 동일해진다.
이것이 Kuhn-Tucker Condition 이다.

#### Kuhn-Tucker Theorem
Let $f, g, 1 \leq i \leq m$ have continuous partial derivatives in an open set containing $x^*$. 
If $x^*$ is a constrained minimum point of $f(x)$ subject to $g_i(x) \leq 0, \; 1 \leq i \leq m$, which satisfies the linear independece constraint qualification condition, then there exists non negative Largrangre multipliers $\lambda_1, \cdots, \lambda_m$ such that
$$
\nabla f(x^*) + \sum_{i=1} \lambda_i \nabla g_i(x^*) = 0 \\
\sum_{i=1}^m \lambda_i g_i (x^*) = 0 \\
\lambda_i \geq 0, \;\;\; 0 \leq i \leq m, \;\;\; \lambda_0 \ne 0
$$
Defining **Largrangian** function by
$$
\phi(x, \lambda) = f(x) + \langle \lambda, g(x) \rangle
$$
where 
$$
\lambda = (\lambda_1, \cdots, \lambda_m)^T, \;\;\;\text{and}\;\;\; g(x) = [g_1(x), g_2(x), \cdots , \cdots g_m(x)]^T
$$

Kuhn-Tucker Theorem은 다음과 같이 간략하게 표시하기도 한다.
$$
\nabla_x \phi(x^*, \lambda) = 0 \\
\langle \lambda, \nabla_{\lambda} \phi(x^*, \lambda) \rangle = 0
$$


## Hamiltononian Method
위에서 논한 제한조건이 있는 최적화 문제를 해결하기 위하여 **Largrangian**을 놓고  **Largrangian Multiplier**를 제한 조건에 곱한 후, Khun-Tucker Condition에 의해 최적화 문제를 해결하는 것을 보았다.

그런데 많은 최적화 문제의 경우 Dynamic System을 최적하게 제어하기 위한 문제가 일반적이다.
Dynamic System의 경우 제한 조건은 Dynamic System의 동역학 그 자체가 제한 조건이 되는데 보통의 경우 시간 $t$에 대한 미분 방정식으로 주어진다.
이때 **시간에 따라 가변하는 시스템을 최적하게 제어/운용** 하기 위한 방법론이 Hamiltonian Method 이다. 


## The Least Action Principle - 최소작용 원리
시간 $t_1$ 에서 $t_2$ 에서의 시스템의 동역학 상태가 각각, A, B 라고 하면 상태 A 에서 B 로의 진화는 다음 적분의 값이 최소가 되도록 진화한다.

$$
S \equiv \int_{t_1}^{t_2} \mathcal{L}(x, \dot{x}, t) dt
$$

이 적분을 시스템의 작용 옥은 Action 이라고 정의하며 적분안의 라그랑지안은 경로에 따라 그 값이 달라지는 경로의 함수이다. 이를 **최소 작용 원리, 혹은 해밀턴의 원리**라고 한다.

## Euler-Lagrange 방정식
방정식
$$
S \equiv \int_{t_1}^{t_2} \mathcal{L}(x, \dot{x}, t) dt
$$

에 대하여 어떤 특정한 경로  가 위 적분 값을 가장 작게 만든다고 가정할 때, 그러한 경로를 만족시키는 미분방정식은
$$
\frac{\partial \mathcal{L}}{\partial x} - \frac{d}{dt}\left(\frac{\partial \mathcal{L}}{\partial \dot{x}} \right ) = 0
$$

### Memorize
$\mathcal{L}$ 을 $x$로 미분후 $\dot{x}$ 미분의 시간에 대한 미분을 뺸다.

### Proof
Let $x(t)$ as follows
$$
x(\alpha, t) = x(t) + \alpha \eta(t)
$$
where $\alpha$ is a parameter when it is 0, $x(t)$  is the minimum phase such as $x(\alpha, t) = x(t)$, $\eta(t)$  is a differentiable function w,r,t time t, that is 0 at end of time , such that $\eta(t_1) = \eta(t_2) = 0$

$\alpha = 0$ 일때 최소값을 가진다면, 모든 임의의 함수에 대하여 다으므이 필요조건이 만족된다.

$$
\frac{\partial S}{\partial \alpha} |_{\alpha=0} = 0
$$

$\alpha$의 미분값은
$$
\frac{\partial S}{\partial \alpha} = \int_{t_1}^{t_2} \frac{d \mathcal{L}}{d \alpha} dt = \int_{t_1}^{t_2} \left( \frac{\partial \mathcal{L}}{\partial x}\frac{\partial x}{\partial \alpha } + \frac{\partial \mathcal{L}}{\partial \dot{x}}\frac{\partial \dot{x}}{\partial \alpha} \right ) dt
$$
여기에서
$$
\frac{\partial x}{\partial \alpha} = \eta, \;\; \frac{dx}{dt} = \frac{\partial x}{\partial t} + \alpha \frac{\partial \eta}{\partial t} \Rightarrow \frac{d}{d \alpha}\left( \frac{dx}{dt} \right)= \frac{\partial \eta}{\partial t}
$$
이므로

$$
\frac{\partial S}{\partial \alpha} = \int_{t_1}^{t_2} \left( \frac{\partial \mathcal{L}}{\partial x}\eta + \frac{\partial \mathcal{L}}{\partial \dot{x}}\frac{\partial \eta}{\partial t} \right ) dt
$$

또한 부분적분에서 
$$
\int \frac{\partial \mathcal{L}}{\partial \dot{x}}\frac{\partial \eta}{\partial t} dt = \frac{\partial \mathcal{L}}{\partial \dot{x}} \eta - \int \frac{d}{dt} \left( \frac{\partial \mathcal{L}}{\partial \dot{x}} \right) \eta dt
$$

$$
\frac{\partial S}{\partial \alpha} = \int_{t_1}^{t_2} \left( \frac{\partial \mathcal{L}}{\partial x}\eta  \right ) dt + \frac{\partial \mathcal{L}}{\partial \dot{x}} \eta |^{t=t_2}_{t=t_1} - \int_{t_1}^{t_2} \frac{d}{dt} \left( \frac{\partial \mathcal{L}}{\partial \dot{x}} \right) \eta dt
$$

이때 중간 항 $\frac{\partial \mathcal{L}}{\partial \dot{x}} \eta |^{t=t_2}_{t=t_1} $ (i.e. \eta(t_0) = \eta(t_1) = 0) $ 이므로 이를 정리하면

$$
\frac{\partial S}{\partial \alpha} = \int_{t_1}^{t_2} \left( \frac{\partial \mathcal{L}}{\partial x}\eta  \right ) dt - \int_{t_1}^{t_2} \frac{d}{dt} \left( \frac{\partial \mathcal{L}}{\partial \dot{x}} \right) \eta dt = 0
$$

**Q.E.D.**

## Largrange 운동 방정식
전체 운동 에너지를  $\mathcal{L}$ 라고 하고 일반화된 좌표계 위에서의 힘을 $Q_0$ 라고 하면


### Lagrange 운동 방정식
$$
\frac{\partial \mathcal{L}}{\partial x} - \frac{d}{dt}\left(\frac{\partial \mathcal{L}}{\partial \dot{x}} \right ) = Q_0
$$

### 보존계의 Largrange 운동 방정식
$$
\frac{\partial \mathcal{L}}{\partial x} - \frac{d}{dt}\left(\frac{\partial \mathcal{L}}{\partial \dot{x}} \right ) = 0
$$

이때, 만일 보존계의 운동 에너지가 $\mathcal{L} = F + \lambda \dot{x}$ 이라고 하면 보존계의 Largrange 운동 방정식에 의해
$$
\begin{align*}
\frac{\partial \mathcal{L}}{\partial \dot{x}} \equiv \lambda \;\;\;\;&: \;\;\;\; \frac{\partial \mathcal{L}}{\partial \dot{x}} = \frac{\partial F}{\partial \dot{x}} (x,t) + \lambda \\
\frac{\partial \mathcal{L}}{\partial x} = \dot{\lambda} \;\;\;\;&: \;\;\;\; \frac{\partial \mathcal{L}}{\partial x} - \frac{d}{dt} \left( \frac{\partial \mathcal{L}}{\partial \dot{x}} \right) = \frac{\partial \mathcal{L}}{\partial x} - \frac{d \lambda}{dt} = 0
\end{align*}
$$
(위에서 $\frac{\partial F}{\partial \dot{x}} (x,t) = 0 $)

### Note
위 공상태 방정식을 기업하는 방법은 Dot 가 어디에 붙어 있는 가 이다.

## Hamiltonian 운동 방정식
Largrangian $\mathcal{L}(x, \dot{x}, t)$ 의 전미분이 다음과 같을 때 (그리고 $\frac{\partial \mathcal{L}}{\partial x} - \frac{d}{dt}\left( \frac{\partial \mathcal{L}}{\partial \dot{x}} \right)) = 0$
$$
d\mathcal{L} = \frac{\partial \mathcal{L}}{\partial x} dx + \frac{\partial \mathcal{L}}{\partial \dot{x}} d{\dot{x}} + \frac{\partial \mathcal{L}}{\partial t} dt
$$
그런데, Largrangian 운동 방정식에서 $\frac{\partial \mathcal{L}}{\partial \dot{x}}=\lambda$ (Largrangian에서 Largange Multiplier는 보통 dx/dt=0 제한조건에서 ) $\frac{\partial \mathcal{L}}{\partial x}= \dot{\lambda}$ (Largrangian 운동 방정식에서 자연스럽게 유도) 이므로

$$
d\mathcal{L} = \dot{\lambda} dx + \lambda d{\dot{x}} + \frac{\partial \mathcal{L}}{\partial t} dt
$$
위 식에 다음을 대입한다.
$$
\lambda d\dot{x} = d(\lambda \dot{x}) - \dot{x} d\lambda
$$
그러면

$$
\begin{align*}
d\mathcal{L} &= \dot{\lambda} dx + d(\lambda \dot{x}) - \dot{x} d\lambda + \frac{\partial \mathcal{L}}{\partial t} dt \\
d(\lambda \dot{x} -\mathcal{L}) &= -\dot{\lambda} dx +  \dot{x} d\lambda - \frac{\partial \mathcal{L}}{\partial t} dt
\end{align*}
$$
여기에서 Hamiltonian 을 다음과 같이 정의한다.
$$
H = \lambda \dot{x} -\mathcal{L}
$$

이렇게 정의하면 위 Hamiltonian 운동 방정식은 다음과 같다.
$$
dH = -\dot{\lambda} dx +  \dot{x} d\lambda - \frac{\partial \mathcal{L}}{\partial t} dt
$$

### Note 
살펴보면 Hamiltonian $H$ 와 적분 경로 $\mathcal{L}$ 은 서로 부호가 반대이다.
이 반대 부호 때문에 공상태 방정식에 있어서 부호가 반대로 나타나는 경우가 발생한다.
(적분 경로에 대해서는 부호가 동일하였다)

## Hamiltonian 운동 방정식 해석
### Largrangian Multiplier 와 Hamiltonian

Hamiltonian $H = \lambda \dot{x} -\mathcal{L}$ 에서 
1. Largrangian Multiplier 에 대하여 Hamiltonian을 미분한 경우
2. 상태 변수 $x$ 에 대하여 Hamiltonian을 미분한 경우
를 각각 살펴보자.

1의 경우는 다음과 같다. (매우 쉽다)
$$
\frac{\partial H}{\partial \lambda} = \dot{x}
$$

2의 경우는 다음과 같다. 다음과 같이 유도된다.
$$
\frac{\partial H}{\partial x} = \frac{\partial}{\partial x}(\lambda \dot{x}) - \frac{\partial \mathcal{L}}{\partial x}
$$
여기서 우변의 첫항은 
$$
\frac{\partial}{\partial x}(\lambda \dot{x}) = \lambda \frac{\partial \dot{x}}{\partial x} =  \lambda \frac{\partial }{\partial x} \frac{\partial x}{\partial t} = \lambda \frac{\partial }{\partial t} \frac{\partial x}{\partial x} = 0
$$
우변의 두번쨰 항은
$$
\frac{\partial \mathcal{L}}{\partial x} = \dot{\lambda}
$$
그러므로 다음과 같다.
$$
\frac{\partial H}{\partial x} = - \dot{\lambda}
$$
이를 **공상태 방정식** 이라 한다.


### Hamiltonian과 Lagrangian 의 차이
결론적으로 보면 일반적인 Largrangian에 추가로 시간에 따른 상태 변화 (시간에 따른 상태의 1계 미분) 에 대한 추가적인 Largrangian 이 붙은 것으로 볼 수 있다.

즉, 다음과 같다.
$$
H = \lambda \dot{x} - \mathcal{L}
$$

그런데 보존계의 운동 에너지가
$$
\mathcal{L} = F + \lambda \cdot \dot{x}
$$

로 주어지면 이는 $H = F$이 된다. 다시말해, Hamiltonian은 보존계의 어떤 에너지가 되어 버린다. 

만일, 시간에 따른 상태 변화가 없는 정상 상태가 된다고 가정하면 ($\dot{x} = 0$) Hamiltonian은 자연스럽게 Largrangian의 운동 에너지가 된다. 그런데, Largrangain 이 well defined 되어 있다고 가정하면, 여기에 상태 변화에 따른 Largrangian Multiplier가 추가된 것으로 볼 수 있다. 

그러므로 만일, **Largrangian**이 well defined 되어 어떤 **상태 변화에 대한 제한 조건이 잡혀 있지 않는 상태**라고 가정하고
**상태 변화에 대한 항만 추가** 되면 이것이 **Hamiltonian** 이 되는 것이다.

이러한 생각을 기반으로 최적 제어 분야에서 Hamiltonian이 적용 된다. (Hamiltonian과 제어 이론)

### Note
정리하면 일반적인 보존계 에너지에 **상태변화에 대한 등식 제한 조건**이 추가되면 **Hamiltonian** 이다.

## Hamiltonian과 제어 이론
상태 방정식이 상태 $x(t)$와 제어 입력 $u(t)$ 그리고 시간 $t$에 의해 다음과 같이 정의된다고 가정하자.
$$
\dot{x}(t) = f(x(t), u(t), t)
$$

이때 Admissable trajectory $x^*$ 가 있어 다음의 Performance Measure를 최소화 시킨다고 가정하자.
$$
J(u) = h(x(t_f), t_f) + \int^{t_f}_{t_0} g(x(t), u(t), t) dt
$$
이와 관련한 Hamiltonian을 유도하는 과정은 다음을 참조한다.[^1]

하지만, 지금까지의 논의를 생각해본다면, 보존계의 에너지를 $g(x(t), u(t), t)$ (왜냐하면 이 값을 최소화 시켜야 하므로) 로 놓고 시간에 따른 상태 변화를 등식 제한조건으로 놓으면 다음과 같이 Hamiltoian을 정의 할 수 있다
$$
\mathcal{H}(x(t),u(t),\lambda, t) = g(x(t), u(t), t) + \lambda f(x(t),u(t), t)
$$

이때 Hamiltonian $\mathcal{H}$의 최적 제어는 다음의 3 조건에서 유도된다.

#### 상태 방정식 조건
$$
\dot{x}^*(t)=\frac{\partial \mathcal{H}}{\partial \lambda}(x(t),u(t),\lambda, t) \\
$$

#### 공상태 방정식 조건
$$
\dot{\lambda}^*(t) = -\frac{\partial \mathcal{H}}{\partial x}(x(t),u(t),\lambda, t)
$$

#### 최적 제어조건
$$
0 = -\frac{\partial \mathcal{H}}{\partial u}(x(t),u(t),\lambda, t)
$$

### Hamiltonian 운동방정식과의 비교
동일하다. 단, 입력 u 에 대한 항이 더 추가 되었다.
1. 상태 방정식 조건
$$
\dot{x} = \frac{\partial H}{\partial \lambda}
$$

2. 공상태 방정식 조건
$$
\dot{\lambda} = - \frac{\partial H}{\partial x}
$$

해당 이론은 최종적으로 Pontryagins's minimum (maximum) Principle 를 통해 완성된다.

#### Note 
항상 기억하자 공상태 방정식 - 상태 방정식과 Dot의 위치는 그대로 있고 편미분의 분모가 $x$ 냐 $\lambda$ 냐에 따라 달라진다. 
기본의 상태방정식이다. 
Hamiltonian 공상태 방정식은 마이너스 부호가 더 붙는다. 
보존계 상태방정식은 $\dot{x}$ 로 편미분하는 것이며 이때 그 결과인 $\lambda$는 당연하게도 dot가 붙지 않는다. 이는 Hamiltonian에서도 동일하다.

## Pontryagins's minimum (maximum) Principle
최적 제어는 반드시, **Hamiltonian을 최소 (혹은 최대) 로 만드는 것이다.** ** 다시말해 다음의 조건을 만족해야 한다.

### Minimum Principle
$$
\mathcal{H}(x^*(t), u^*(t), \lambda^*, t) \leq \mathcal{H}(x^*(t), u(t), \lambda^*, t)
$$
상태와 Largrangian multiplier가 최적이라 하더라도 **입력이 최소값을 만들 수 있어야 한다.**

### Maximum Principle
$$
\mathcal{H}(x^*(t), u^*(t), \lambda^*, t) \geq \mathcal{H}(x^*(t), u(t), \lambda^*, t)
$$
어떤 효용을 극대회 시키는 것으로 해석할때 이렇게 된다.







### Note
결론적으로
$$
\frac{\partial \mathcal{H}}{\partial u} = 0
$$

이어야 한다는 의미이다. 그런데 이는 Necessary Condition이기 때문에 극대와 극소를 모두 포함한다.

그러므로 Pontryagins's minimum (maximum) Principle 에 의해 최소(최대)화 시키는 제어는 반드시 그렇지 않은 제어값보다 작거나(크거나) 해야 하는 것이다.
