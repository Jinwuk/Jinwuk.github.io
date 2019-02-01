Change of Probablity Measure
============================

[TOC]

## Radon-Nykodym Theorem
### Prequal
확률 측도 공간 $(\Omega, \mathcal{F}, \mathbb{P})​$ 위에서 주어진 $f \geq 0​$ 이 가측이고 적분 가능할 때, 임의의 $E \in \mathcal{F}​$ 에 대하여 

$$
\mathbb{Q}(E) = \int_{E} f d\mathbb{P} = \mathbb{E}[1_E f]
$$

라고 정의하면 $\mathbb{Q}$는 $(\Omega, \mathcal{F})$ 위에서 정의된 측도이다. 특히 $\mathbb{E}[1_E f] = 1$이면 $\mathbb{Q}$는 확률 측도이다. 

### Absolutely Continuous Measure (절대 연속 측도)
1. 가측공간 $(\Omega, \mathcal{F})$ 위에서 측도 $\mathbb{P}, \mathbb{Q}$ 가 주어졌을 때, 만일 $E \in \mathcal{F}$ 에 대하여 $\mathbb{P}(E) = 0$ 이면 언제나 $\mathbb{Q}(E) = 0$ 일때, $\mathbb{Q}$는 $\mathbb{P}$에 대하여 절대 연속이고 $Q \ll P​$ 이다 

2. 대표적으로 $\mathbb{Q}(E) = \mathbb{E}[1_E f]$ 이면 $\mathbb{E}[1_E f]$ 이 $\mathbb{P}$ 에 의해 구해졌으므로 당연히 $\mathbb{Q} \ll \mathbb{P}$ 이다.

3. **equivalent** : if $Q \ll P$ and $P \ll Q$ 이면 $P$와 $Q$는 동등하며 $P \approx Q$

### Radon-Nykodym Theorem
가측 공간 $(\Omega, \mathcal{F})$ 위에서 두개의 측도   $\mathbb{P}, \mathbb{Q}$ 가 주어질떄, if  $Q \ll P$  (절대 연속 측도) 이면 0 이상의 값을 가지는 (Positive Semi Definite) 가측 함수 $f : \Omega \rightarrow \mathbb{R}$ 이 존재하여 임의의 $E \in \,mathcal{F}$ 에 대하여 
$$
\mathbb{Q}(E) = \int_{E} f d\mathbb{P}
$$
가 성립한다. 이때, $f$를 $\mathbb{P}$ 에 대한 $\mathbb{Q}$ 의 밀도함수로 생각하여 이를 **Radon-Nykodym Derivative** 라고 부르며 
$$
f = \frac{d\mathbb{Q}}{d\mathbb{P}}
$$
이다. 

#### Notice 
1.  $\mathbb{P}, \mathbb{Q}$ 가 확률 측도라면 임의의 가측함수 (확률변수) $X:\Omega \rightarrow \mathbb{R}$ 에 대하여 
$$
\mathbb{E}^{\mathbb{Q}}(X) = \mathbb{E}(X \frac{d\mathbb{Q}}{d\mathbb{P}})
$$
왜냐하면 E가 적분이기 때문이다. 
2. 다음이 성립한다.
$$
\frac{d\mathbb{Q}}{d\mathbb{P}} = \left(\frac{d\mathbb{P}}{d\mathbb{Q}} \right)^{-1}
$$
3. 옵션 가격 이론에서 주가가 실제로 가지는 확률분포를 $\mathbb{P}$ 라고 하면 이것과 동등한 확률분포 $\mathbb{Q}$ 를 사용하여 옵션의 기대값을 구한다.
   - 이는 다른 분야에 얼마든지 적용할 수 있다. 예를 들어 데이터의 분포를 $\mathbb{P}$ 라 할때 이것에 대한떠 어떤 Transform 에 대한 분포를 구하는 방식이다.

## Martingale 
### Filtration 
$\Omega$ 위의 $\sigma$-algebra $\{\mathcal{F}_t\}_{t \in A}$ 가 if $ s \leq t$ 인 $s,t \in A$ 에 대하여 

$$
\mathcal{F}_s \subset \mathcal{F}_t \subset \mathcal{F}
$$

이면 $\{\mathcal{F}_t\}_{t \in A}$ 는 **Filtration** 이다.

### Martingale
Stochastic Process $\{\xi_t \}_{r \in A}$ 가 아래의 조건을 만족하면 
1. 임의의 $t$에 대하여 $\xi_t : (\Omega, \mathbb{P}) \rightarrow \mathbb{R}$은 적분 가능하다.
2.  $\{\xi_t \}_{r \in A}$ 는 Filtration  $\{\mathcal{F}_t\}_{t \in A}$ 에 Adaptive 되어 있다.
   - 즉, 임의의 $t$ 에 대하여 $\xi_t : \Omega \rightarrow \mathbb{R}$ 가 $\mathcal{F}_t$ 가측이다.
3. 임의의 $s \leq t$ 에 대하여 $\xi_s = \mathbb{E}(\xi_t|\mathcal{F}_s)$  

3번이 바로 Martingale의 실제적 정의다.

따라서 만일 $(\Omega, \mathbb{P}, \mathcal{F}_t)$ 에 대하여 $\{ F_t\}_{0 \leq t \leq T}$ 와 $\mathcal{F}_T$ 가측인 확률변수 $X$가 주어졌을 떄

$$
M_t = \mathbb{E}(X|\mathcal{F}_t)
$$

이면 $\{M_t\}_{0 \leq t \leq T}$는 Martingale 이다.

## Girsanov Theorem

Girsanov Theorem에 대해서는 Fast Proof를 생각해 보았으나 기존의 접근 방법으로는 Fast Proof를 만들 수 없다. 가장 큰 이유는 기존의 방법론들이 Random Variable에 대한 접근 방법이지만, Girsanov theorem의 방법은 PDF 자체에 대한 접근이기 때문에 Proof 방법론이 다르다. 이 방법론은 그러므로 다르게 접근하여야 한다. 
Girsanov Theorem에 대하여 접근하기 전에 먼저 Levy's Theorem을 먼저 Check한다. 


### Levy's Theorem

Let $X_t = \left(X_1 (t), \cdots X_n (t) \right)$ be a continuous stochastic process on a probability space $(\Omega, \mathcal{H}, Q)$ with values in $\textbf{R}^n$. Then the following 1) and 2) are equivalent

1. $X_t$ is a Brownian Motion w.r.t. $Q$, i.e. the law of $X_t$ w.r.t. $Q$ is the same as the law of an n-dimensional Brownian Motion,
2. 1) $X_t = \left(X_1 (t), \cdots X_n (t) \right)$  is a martingale w.r.t. $Q$ (and w.r.t. its own filtration) and
   2) $X_i (t) X_j (t) - \delta_{i,j} t$ is a martingale w.r.t. $Q$ for all $i,j, \in \{1, 2, \cdots, n \}$

### Exponential Martingale
Suppose $\theta(t,w) = \left( \theta_1 (t,w), \cdots, \theta_n (t,w) \right) \in \textbf{R}^n$ with $\theta_k (t,w) \in \Lambda [0,T]$ for $k=1, \cdots, n$ where $T \leq \infty$. Define

$$
Z_t = \exp \left( \int^t_0 \theta(s,w) dB(s) - \frac{1}{2} \int^t_0 \theta^2 (s,w) ds \right); \;\;\; 0 \leq t \leq T
$$

where $B(s) \in \textbf{R}^n$ and $\theta^2 = \theta \cdot \theta$ (dot product)
then 

$$
dZ_t = Z_t \theta (t,w) dB(t)
$$

#### Proof
Set the function $f(t,x)$ such that

$$
f(t,x) = \exp \left( \int^x_0 \theta(s,x) dx - \frac{1}{2} \int^t_0 \theta^2 (s,x) ds \right); \;\;\; 0 \leq t \leq T
$$

and $X_t = B_t$ such that $dX_t = dB_t$
By Ito's Formula

$$
\begin{align}
dZ_t = df(t,x)|_{x=B_t} &= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x}dx + \frac{1}{2}\frac{\partial^2 f}{\partial x^2} (dx)^2 |_{x=B_t} \\
&= \left( \frac{\partial f}{\partial t} + \frac{1}{2}\frac{\partial^2 f}{\partial x^2} \right) dt + \frac{\partial f}{\partial x}dB_t  
\end{align}
$$

그러므로

$$
\begin{align}
\frac{\partial f}{\partial t} &= -\frac{1}{2} \theta^2 (t,x) f(x,t)\\
\frac{\partial f}{\partial x} &= \theta (t,x) f(x,t)\\
\frac{\partial^2 f}{\partial x^2} &= \frac{\partial f}{\partial t}(\theta (t,x) f(x,t)) = \theta^2 f(x,t)
\end{align}
$$

따라서

$$
dZ_t = Z_t \theta (t,w) dB_t
$$

#### Remarks
$Z_t$가 다음과 같이 $dB_s$의 적분항이 (-) 이더라도 결과는 동일하다. 이 경우엔 function $f(t,x)$를 동일한 부호가 되도록 잡는다.

$$
Z_t = \exp \left( -\int^t_0 \theta(s,w) dB(s) - \frac{1}{2} \int^t_0 \theta^2 (s,w) ds \right); \;\;\; 0 \leq t \leq T
$$

왜냐하면 2차 미분항의 결과를 보면 

$$
\frac{\partial^2 f}{\partial x^2} = \frac{\partial }{\partial x} (-\theta f) = -\theta \cdot -\theta f = \theta^2 f
$$

로 동일해지기 때문이다.

### Kazamaki Condition 
A sufficient condition that $Z_t$ be a martingale is 

$$
\mathbb{E}[\exp(\frac{1}{2} \int^t_0 \theta (s,w) dB_s)] < \infty \;\;\; \forall t \leq T
$$

### Novikov Condition (Stronger Condition of Kazamaki Condition)

$$
\mathbb{E}[\exp(\frac{1}{2} \int^T_0 \theta (s,w) dB_s)] < \infty 
$$

즉, 두 조건 모두 EXponential Process가 t에 대하여 Normalized 되면 Martingale 이라는 의미이다.

### Concept of Girsanov Theorem
Simple 이지만 거의 완벽하게 Girsanov Theorem을 설명할 수 있다.
Let $\{W_t \}_{t \geq 0}$ be a $\mathbb{P}$-Brownian Motion. For a constant value $\theta$, consider the new stochastic Process $X_t$ such that

$$
X_t = W_t + \theta t 
$$

이것이 다음을 만족할 수 있어야 한다.

$$
\int_{\Omega} f(W_t(w)) d\mathbb{P}(w) = \int_{\Omega} f(X_t (w)) d\mathbb{Q}(w) = \int_{\Omega} f(W_t (w) + \theta t) d\mathbb{Q}(w)
$$

그런데, $\{W_t \}_{t \geq 0}$ is a $\mathbb{P}$-Brownian Motion 이므로 $f(x)=1_{I}(x)$ 라고 하면  동일한 사건집합 $\Omega$ 에 대해서 동일한 평균값이 나와야 한다. 그러므로 

$$
\int_{\Omega} f(W_t(w)) d\mathbb{P}(w) = \int_{\Omega} \frac{1}{\sqrt{2 \pi} t} \exp(-\frac{x^2}{2t}) dx
$$

로 볼 수 있고 이에 대해

$$
\int_{\Omega} f(X_t (w)) d\mathbb{Q}(w) = \int_{\Omega} f(W_t (w) + \theta t) d\mathbb{Q}(w) = \int_{\Omega} \frac{1}{\sqrt{2 \pi} t} \exp(-\frac{(x + \theta t)^2}{2t}) dx
$$

이다. 
$\mathbb{P}$에 대한 $\mathbb{Q}$의 Radon-Nykodym 도함수를 

$$
L(w) = \frac{d\mathbb{Q}}{d\mathbb{P}}(w)
$$

라 하고 $\mathbb{E}[L | \mathcal{F}_t] = L_t$ 라고 하자. 이때, 함수 $L_t$가 각각의 t에 대하여 함수 $\rho_t : \textbf{R} \rightarrow \textbf{R}$ 이 존재하여 다음과 같다고 하자.

$$
 L_t(w) = \rho_t(W_t (w))
$$

이때 다음을 증명 하는 것이다.

$$
\mathbb{E}^{\mathbb{P}}(1(W_t)) = \mathbb{E}^{\mathbb{Q}}(1(X_t))
$$

이를 전개해 보면

$$
\begin{align*}
\mathbb{E}^{\mathbb{P}}(1(W_t)) = \int_{\Omega} 1(W_t) d\mathbb{P}  &= \int_{\Omega} 1(X_t) d\mathbb{Q} = \mathbb{E}^{\mathbb{Q}}(1(X_t))\\
&= \int_{\Omega} 1(W_t) \frac{d\mathbb{Q}}{d\mathbb{P}}d\mathbb{P} \;\;\;\text{측도가 }\mathbb{P}\text{로 바뀌어 }X_t\text{가 } W_t\text{로 바뀐다}\\
&= \int_{\Omega} 1(W_t) L_t d\mathbb{P} \\
&= \int_{\Omega} \rho_t (x) \frac{1}{\sqrt{2 \pi} t} \exp(-\frac{x^2}{2t}) dx
\end{align*}
$$

또한 

$$
\int_{\Omega} 1(X_t) d\mathbb{Q} = \int_{\Omega} \frac{1}{\sqrt{2 \pi} t} \exp(-\frac{(x + \theta t)^2}{2t}) dx
$$

이므로 이를 정리하면

$$
\rho_t (x) \exp(-\frac{x^2}{2t}) = \exp(-\frac{(x + \theta t)^2}{2t})
$$

에서

$$
\rho_t (x) = \exp(-\theta x - \frac{1}{2} \theta^2 t)
$$

$L_t (w)$는 그러므로

$$
L_t(w) = \rho_t (W_t(w)) = \exp(-\theta W_t - \frac{1}{2} \theta^2 t)
$$

## Research of Girsanov Theorem

### 1. Expectation
Girsanove Theorem은 결국 Radon-Nykodym Derivative가 다음과 같을 때

$$
L_t = \frac{d\mathbb{Q}}{d\mathbb{P}} =  \exp(-\theta W_t - \frac{1}{2} \theta^2 t)
$$

즉, Radon-Nykodym Derivative가 Exponential Normalized Brownian Motion 이라는 의미이다. 
이를 조금 풀어 쓰면

$$
d \mathbb{Q} = L_t d \mathbb{P}
$$

이므로 적분에 자동으로 $L_t$ 가 들어간다는 의미이다. 즉, Expecatation Value 계산에 $L_t$ 가 들어간다는 의미이다.
즉. 다음과 같다는 의미이다.

$$
\mathbb{E}^{\mathbb{Q}}(X_t) = \mathbb{E}^{\mathbb{P}}(L_t W_t)
$$

### 2. Exponential Random Process

앞에서 $X_t = W_t + \theta t $ 인데, 이를 다시 생각해 보면 $X_t$ 는 $W_t$ 를 $\theta t $ 만큼 이동 시킨 후 이를 다시 $W_t$의 Probablity 로 평균값을 구한다는 의미이다. 이것은  $L_t$라는 Normalized Exponrntial Stochastic Process에 $W_t$의 측도를 곱한 것이 된다는 의미이다. 결국 최종적으로 생각해 보면, $x = W_t$ 에서 $-\frac{x^2}{2t}$ 때문에 Normalized Exponential Process가 유도되는 원리이다.

### 3.Martingale Property

$L_t = \exp(-\theta W_t - \frac{1}{2} \theta^2 t)$ 일때  확률측도 $\mathbb{Q}$를 다음과 같이 정의한다.

$$
\frac{d\mathbb{Q}}{d\mathbb{P}}|_{\mathcal{F}_t} = L_t
$$

#### Theorem 3.1
$\phi_t$ 가 $\mathcal{F}_t$ 가측 함수 일때 다음이 성립한다.

$$
E^{\mathbb{Q}}[\phi_t | \mathcal{F}_s] = E^{\mathbb{P}}[\phi_t \frac{L_t}{L_s}|\mathcal{F}_s]
$$

#### Corollary 
1. $s=0$ 이면 당연하지만 (그리고 1.Expectation에서 나온 결과와 동일하다.)

$$
E^{\mathbb{Q}}[\phi_t ] = E^{\mathbb{P}}[\phi_t L_t]
$$

2. $s=0$ 이고 $\phi_t$가 1이면 

$$
E^{\mathbb{Q}}[1] = E^{\mathbb{P}}[L_t]=1
$$

3. $\phi_t$가 1이면 

$$
\begin{align*}
1 = E^{\mathbb{Q}}[1|\mathcal{F}_s] &= E^{\mathbb{P}}[\frac{L_t}{L_s}|\mathcal{F}_s]\\
E^{\mathbb{P}}[L_t | \mathcal{F}_s] &= L_s
\end{align*}
$$

#### Remarks 
1. $E^{\mathbb{Q}}[X_t] = 0$

$$
\begin{align*}
E^{\mathbb{Q}}[X_t] &= E^{\mathbb{P}}[(W_t + \theta t)L_t] \\
&= E^{\mathbb{P}}[(W_t + \theta t)e^{-\frac{1}{2}\theta^2 t - \theta W_t}] \\
&= e^{-\frac{1}{2}\theta^2 t} E^{\mathbb{P}}[(W_t + \theta t) e^{-\theta W_t}] \\
&= e^{-\frac{1}{2}\theta^2 t} (E^{\mathbb{P}}[W_t e^{-\theta W_t}]  + E^{\mathbb{P}}[\theta t e^{-\theta W_t}]) \\
&= e^{-\frac{1}{2}\theta^2 t} (-\theta t e^{-\frac{1}{2}\theta^2 t} + \theta te^{-\frac{1}{2}\theta^2 t}) \\
&= 0 
\end{align*}
$$

2. $E^{\mathbb{Q}}[X^2_t] = t$ ($\mathbb{P}$는 자명하므로 생략한다.)

$$
\begin{align*}
E^{\mathbb{Q}}[X^2_t] &=  E[(W_t + \theta t)^2 e^{-\frac{1}{2} \theta^2 t - \theta W_t}] \\
&=  E[W^2_t e^{-\frac{1}{2} \theta^2 t - \theta W_t}]+ 2 \theta t E[W_t e^{-\frac{1}{2} \theta^2 t - \theta W_t}] + (\theta t)^2 E[e^{-\frac{1}{2} \theta^2 t - \theta W_t}]  \\
&= e^{-\frac{1}{2} \theta^2 t}\left(E[W^2_t e^{-\theta W_t}] + 2 \theta t E[W_t e^{-\theta W_t}] + (\theta t)^2 E[ e^{-\theta W_t}] \right) \\
&= e^{-\frac{1}{2} \theta^2 t} \left((t+\theta^2 t^2) e^{-\frac{1}{2} \theta^2 t} - 2 (\theta t)^2 e^{-\frac{1}{2} \theta^2 t} + (\theta t)^2 e^{-\frac{1}{2} \theta^2 t} \right) \\
&= t
\end{align*}
$$

## Brownian Motion to new probability measure
Assume that $X_t = W_t + \theta t$ 

### Lemma 1.
$X_t$는 $\mathbb{Q}$-Martingale 이다. 
#### proof
Let $L_t = \exp \left( -\frac{1}{2} \theta^2 t - \theta W_t \right)$ 

$$
E[W_t L_t | \mathcal{F}_s] = E[W_t e^{( -\frac{1}{2} \theta^2 t - \theta W_t) } | \mathcal{F}_s] = e^{-\frac{1}{2}\theta^2 t} E[W_t e^{-\theta W_s}|\mathcal{F}_s]=\left( W_s - \theta (t -s) \right) L_s
$$

Since $E^{\mathbb{Q}}[\Phi_t|\mathcal{F}_s]= E[\Phi_t L_t L_s^{-1} | \mathcal{F}_s]$

$$
\begin{align*}
E^{\mathbb{Q}}[X_t|\mathcal{F}_s] &= E[X_t L_t L_s^{-1} | \mathcal{F}_s] \\
&= L_s^{-1}E[(W_t + \theta t)L_t | \mathcal{F}_s] \\
&= L_s^{-1}\left( E[W_t L_t | \mathcal{F}_s] + \theta t E[ L_t | \mathcal{F}_s] \right) \\
&= L_s^{-1} L_s (W_s - \theta (t-s)) +  L_s^{-1} L_s \theta t \\
&= W_s + \theta s =X_s
\end{align*}
$$

### Lemma 2.
$X_t^2 - t $는 $\mathbb{Q}$-Martingale 이다. 
#### proof
Let $L_t = \exp \left( -\frac{1}{2} \theta^2 t - \theta W_t \right)$ 

$$
E[W_t^2 L_t | \mathcal{F}_s]=e^{-\frac{1}{2}\theta^2 t}E[W_t^2 e^{-\theta W_t}|\mathcal{F}_s]=\left( (t-s)+(W_s - \theta(t-s)^2) \right)L_s
$$

Therefore,

$$
\begin{align*}
E^{\mathbb{Q}}[X_t^2 - t | \mathcal{F}_s] &= E[X_t^2 L_t L_s^{-1}| \mathcal{F}_s] - t\\
&=L_s^{-1}E[(W_t+\theta t)^2 L_t | \mathcal{F}_s] - t \\
&=L_s^{-1}\left(E[W_t^2 L_t | \mathcal{F}_s] + 2 \theta t E[W_t L_t | \mathcal{F}_s] + \theta^2 t^2 E[L_t | \mathcal{F}_s]\right) - t \\
&=L_s^{-1} L_s\left( (t-s)+(W_s - \theta(t-s)^2) \right) + 2L_s^{-1} L_s \theta t \left(W_s + \theta(t-s) \right) +L_s^{-1} L_s \theta^2 t^2 - t \\
&= (W_s + \theta s)^2 -s = X_s^2 -s
\end{align*}
$$

### Girsanov Theorem
$\{W_t \}_{t \geq 0}$ 는 $\mathbb{P}$-Brownian Motion 이고 $\theta$는 임의의 실수이고 $X_t=W_t + \theta t$ 일떄 확률측도 $\mathbb{Q}$가 임의의 $0 \leq t \leq T$에 대하여 다음과 같은 성질을 지닌 측도라고 정의하면 

$$
L_t = \frac{d\mathbb{Q}}{d\mathbb{P}}|_{\mathcal{F}_t} = e^{-\frac{1}{2}\theta^2 t - \theta W_s}
$$

이때, 두 측도 $\mathbb{P}$, $\mathbb{Q}$ 는 서로 동등하며 $\{X_t \}_{t \geq 0}$ 는 $\mathbb{Q}$-Brownian Motion 이다.

####  proof
Levy's Theorem 1, 2 에서 특히 2항의 1, 2, 는 각각 Lemma 1,2 를 통해 증명되고 1 은 앞에서 증명되었으므로 위 Thorem은 증명된다.

앞에서 단순한 형태의 stochastic Process에 대한 Girsanov Theorem을 알아보았다. 이번에는 보다 일반적인 형태의 SDE 에서의 Girsanov Theorem을 생각해 보도록 한다.

들어가기전에 간단한 형태의 Random Process에 대하여 생각해보자.
$X_t$ 는 $N(\mu_1, \sigma_1)$ 분포를 $P$ Measure 하에서 가진다고 가정할 때 $X_t$ 가 $N(\mu_2, \sigma_2)$ 분포를 $P$ Measure 하에서 가지기 위해서는 다음의 관계를 만족해야 한다.

$$
\frac{dQ}{dP}(X_t) = \Lambda(X_t) = \frac{\sigma_1}{\sigma_2}e^{\frac{(x-\mu_1)^2}{2\sigma^2_1}-\frac{(x-\mu_2)^2}{2\sigma^2_2}}
$$

이다. 이는 간단히 증명된다. (Since $Q$하에서 $N(\mu_2, \sigma_2)$ 이기 위해서는 $\frac{1}{\sqrt{2\pi} \sigma_2 }e^{-\frac{(x-\mu_2)^2}{2\sigma^2_2}}$ 이어야 하므로 $P$ 의 분포가 역수로 들어가게 된다. 어차피 exp를 미분해도 exp 함수는 남는다.)

## Pre-Definition
### Theorem : General Bayes Formula
Let $\mathcal{G}$ be a sub-$\sigma$-field of $\mathcal{F}$ on which two probablity measure $Q$ and $P$ are defined. If $Q << P$ with $dQ = \Lambda dP$ and $X$ is $Q$-integrable, then $\Lambda X%$ is $P$-integrable and $Q$-a.s.

$$
E_Q(X|\mathcal{G}) = \frac{E_p(X\Lambda|\mathcal{G})}{E_P(X|\mathcal{G})}
$$

#### proof

$$
E_Q(\xi X)= E_Q(\xi E_Q(X|\mathcal{G}))
$$

이므로 

$$
\begin{align*}
E_Q\left( \frac{E_P(X \Lambda | \mathcal{G})}{E_P(\Lambda | \mathcal{G})} \xi \right)
&= E_P\left(\Lambda \frac{E_P(X \Lambda | \mathcal{G})}{E_P(\Lambda | \mathcal{G})} \xi \right) \\
&= E_P\left(E_P(\Lambda | \mathcal{G}) \frac{E_P(X \Lambda | \mathcal{G})}{E_P(\Lambda | \mathcal{G})} \xi \right) \\
&=E_P(E_P(X \Lambda | \mathcal{G}) \xi) = E_P(X \Lambda \xi) = E_Q(X\xi)
\end{align*}
$$

그러므로 

$$
E_Q(\xi X)= E_Q(\xi E_Q(X|\mathcal{G})) = E_Q\left( \frac{E_P(X \Lambda | \mathcal{G})}{E_P(\Lambda | \mathcal{G})} \xi \right)
$$

관계에서 증명 끝

### Theorem 2
$dQ/dP = \Lambda(T)$ 일떄 

$$
E_Q(X|\mathcal{F}_s) = E_P \left( X \frac{\Lambda(t)}{\Lambda(s)}|\mathcal{F}_s \right)
$$

### Theorem : Girsanov Theorem for Brownian Motion
- Let $B(t), 0 \leq t \leq T$, be a Brownian Motion under probability measure $P$. (**$B(t)$는 $P$ measure**)
- Consider the process 

$$
W(t) = B(t) + \mu t
$$

- Define the measure $Q$ by

$$
\Lambda = \frac{dQ}{dP}(B_{[0, T]})= \exp (-\mu B(T) - \frac{1}{2} \mu^2 T)
$$

  where $B_{[0, T]}$ denotes a path of Brownian motion on $[0,T]$. Then $Q$ is equivalent to $P$ , and **$W(t)$ is a $Q$- Brownian motion.**

$$
\Lambda = \frac{dP}{dQ}(W_{[0, T]})= \exp (\mu W(T) - \frac{1}{2} \mu^2 T)
$$



### Theorem : Girsanov Theorem for Removal of Drift

Brownian Motion의 경우 Girsanov Theorem은 이미 앞에서 살펴보았다.
**Drift가 없는 경우의 Girsanov Theorem**은 다음과 같다.
Let $B(t)$ be a $P$-Brownian motion, and $H(t)$ is such that 

$$
X(t)=-\int_0^t H(s)dB(s) \;\;\textit{or}\;\; dX_t = H(t)dB_t
$$

Moreover $\mathcal{E}(X)$ is a martingale. Define an equivalent measure $Q$ by

$$
\Lambda = \frac{dQ}{dP}(B) = \exp (-\int^T_0 H(s) dB(s) - \frac{1}{2}\int H^2(s)ds) = \mathcal{E}(X)(T).
$$

Then the process

$$
W_t = B_t + \int^t_0 H(s) ds 
$$

is a $Q$-Brownian Motion

위의 결과를 사용하여 간략히 생각해보면 다음과 같다.

### Theorem : Simple Concept

Let $M_1(t), 0 \leq t \leq T$ be a continous **$P$-martingale**. Let **$X_t$ be a continuous $P$-martingale** such that $\mathcal{E}(X)$ is a martingale. Define a new probablity measure $Q$ by

$$
\frac{dQ}{dP} = \Lambda = \mathcal{E}_T = e^{X_T - \frac{1}{2}[X,X]_T}
$$

Then 

$$
M_2(t) = M_1(t) - [M, X]_t
$$

is **a continuous martingale under $Q$**

여기에서 일반적인 형태의 Girsanov Theorem을 살펴본다.

## Change of Drift in Diffusions
Let $X_t$ be a diffusion, so that with a P-Brownian motion $B_t$, $X_t$ satisfies the following stochastic differential equation wothj $\sigma(x,t) > 0$

$$
dX_t = \mu_1 (X_t, t)dt + \sigma(X_t, t)dB_t
$$

Let

$$
H_t = \frac{\mu_1(X_t,t) - \mu_2(X_t, t)}{\sigma(X_t, t)}
$$

and define $Q$ by $dQ = \Lambda dP$ with

$$
\Lambda = \frac{dQ}{dP} = \mathcal{E}(-\int^{\cdot}_{0}H_t dB_t ) = e^{-\int^T_0 H_t dB_t - \frac{1}{2}\int^T_0 H^2_t dt}
$$

By Girsanov Theorem, provided the process $\mathcal{E}(H \cdot B)$ is a martingale, the process

$$
W_t = B_t + \int^t_0 H_s ds
$$

is a $Q$-Brownian motion. But

$$
dW_t = dB_t + H_t dt = dB_t + \frac{\mu_1(X_t,t) - \mu_2(X_t, t)}{\sigma(X_t, t)} dt
$$

Rearranging, we obtain the equation for $X_t$

$$
dX_t = \mu_2(X_t, t)dt + \sigma(X_t,t)dW_t
$$

with a $Q$-Brownian motion $W_t$

### Basic Idea
즉, Girsanov Theorem은 Brownian Motion에 관한 내용이므로 Diffusion Process $X_t$ 가 서로다른 Measure를 가진 Brownian Motion에서 동일하게 나타나야 하므로 다음의 관계를 만족한다.

$$
\mu_1(X_t,t)dt + \sigma(X_t,t)dB_t = \mu_2(X_t,t)dt + \sigma(X_t,t)dW_t  
$$

그러므로

$$
\begin{align*}
(\mu_1(X_t,t) - \mu_2(X_t,t))dt +  \sigma(X_t,t)dB_t &= \sigma(X_t,t)dW_t \\
\frac{\mu_1(X_t,t) - \mu_2(X_t,t)}{ \sigma(X_t,t)}dt + dB_t &= dW_t \\
H_t dt + dB_t &= dW_t \\
\end{align*}
$$

따라서

$$
W_t = B_t + \int^t_0 H_s ds
$$

이로서 **Brownian Motion 만의 관계로 정리한다.**

### Notice
1. 결국 stochastic differential equation 에서 중요한 것은 Brownian motion $B_t$ 혹은 $W_t$ 가 측도가 변하더라도 계속 그에 맞는 측도에 따라 **Brownian motion**이 되어야 한다는 것이다.
2. 따라서 Drift 부분은 Girsanov Theorem의 관심대상이 아니다. $W_t = B_t + \int \theta(t) dt$ 와 같이 되더라도 계속 Brownian motion으로 남아 있도록 $dQ = \Lambda dP$ 가 되도록 하는 $\Lambda$ 가 존재하면 SDE는 결국 똑같은 SDE가 된다.
3. 앞절에서 살펴본 $X_t = W_t + \theta t $의 형태는 일반적인 형태에서 $X_t = W_t + \int^t_0 H(s) ds$ 의 형태가 되는 것이다. 즉, $dW_t = dB_t + H(s)ds$ 인 것이다. 결국 **변형된 Wiener Process에 대한 SDE의 Consistency 조건**이 바로 Girsanov Theorem이다.
4. Drift가 변하는 경우에 대하여 간략히 생각해보면 먼저 $dW_t$에 대한 Drift 변화를 Scaling 해서 $dB_t$에 대한 Drift로 바꾸고 이에 따른 $dW_t$ 항의 변화치를 가지고 Girsanov Theorem을 적용하는 것이다.
   - 결론적으로 Brownian Motion을 다르게 정의하여 Measure가 변화할 경우 Drift가 변하여야 한다. Drift가 변화하지 않는 경우에는 Brownian Motion이 변화할 수 없다.
5. Wiener Process가 $dB_t$ 에서 $dW_t = dB_t + H_t dt$ 의 형태라고 하면 Girsanov Theorem에 의해

$$
\frac{dQ}{dP}=\Lambda = e^{-\int^t_0 H_s dB_s - \frac{1}{2}\int^t_0 H^2_s ds}
$$

즉, $[B_t H_t] = \int^t_0 H_s dB_s$ process와 Normalized factor $- \frac{1}{2} \int^t_0 H^2_s ds$로 구성된다는 것을 알 수 있다. 즉, Normalized Exponential Process로 측도를 변화시키면 된다는 뜻이다.

이는 앞절에서 $\exp(-\theta W_t - \frac{1}{2} \theta^2 t)$와 동일한 의미이다. $\theta$ 가 함수가 아닌 상수라서 이러한 표현이 나타난 것일 뿐이다. 
즉, $\exp(-\int^t_0 \theta(s)dW_s - \frac{1}{2} \int^t_0 \theta^2(s) ds)$ 로 표현해도 같은 것이다.

## Likelihood Functions
일반적인 형태의 Girsanov Theorem의 가장 좋은 Application중의 하나는 Likelihood 이다. 
이것의 개념은 만일 두 모델 P, Q 가 있고 이것의 Normalized 적합성을 각각 $P, Q$ 라 하면, Radon-Nykodym Derivation에 의한 $\Lambda = dQ/dP  $ 를 통해 Likelihood를 계산해 내는 것이다. 
**The Likelihood is the Radon-Nykodym Derivative $\Lambda = dQ/dP  $**

### Likelihood ratio for Diffusions

SDE with $dB_t, \, P$-Brownian Motion : $dX_t = \mu_1(X_t, t) dt + \sigma(X_t, t) dB_t$
SDE with $dW_t, \, Q$-Brownian Motion : $dX_t = \mu_2(X_t, t) dt + \sigma(X_t, t) dW_t$

Drift가 서로 다르므로 앞에서와 마찬가지로 다음과 같은 Scaling Function을 도입한다.

$$
H_t = \frac{\mu_2(X_t,t) - \mu_1(X_t, t)}{\sigma(X_t, t)}
$$

이 경우, Radon-Nykodym Derivative $\Lambda$ 는 다음과 같다.

$$
\Lambda(X_{[0,T]}) = \frac{dQ}{dP} = \exp\left(\int^T_0 H_t dB_t - \frac{1}{2} \int^T_0 H^2_t dt \right)
$$

이를 풀어서 쓰면 다음과 같다.

$$
\Lambda(X_{[0,T]}) = \frac{dQ}{dP} = \exp\left(\int^T_0 \frac{\mu_2(X_t,t) - \mu_1(X_t, t)}{\sigma(X_t, t)} dB_t - \frac{1}{2} \int^T_0 \left(\frac{\mu_2(X_t,t) - \mu_1(X_t, t)}{\sigma(X_t, t)}\right)^2 dt \right)
$$

그런데 실제로 관측되는 Process는 보통 $X_t$ 이다. ($B_t$는 가상의 프로세스이기는 하다.) 그러므로 실제로 위 값을 계산하기 위해서는 $dB_t$항을 $x_t$항의 적분으로 바꾸어야 한다. 이는 결국

$$
dB_t = \frac{dX_t - \mu_1(X_t,t)dt}{\sigma(X_t, t)}
$$

이를 적분항에 대입하여 정리하면

$$
\int^T_0 \frac{\mu_2(X_t,t) - \mu_1(X_t, t)}{\sigma(X_t, t)} \cdot \frac{dX_t - \mu_1(X_t,t)dt}{\sigma(X_t, t)} = \int^T_0 \frac{\mu_2(X_t,t) - \mu_1(X_t, t)}{\sigma^2(X_t, t)}dX_t - \int^T_0 \frac{\mu_1(X_t, t)\mu_2(X_t,t) - \mu^2_1(X_t, t)}{\sigma^2(X_t, t)}dt
$$

따라서 Radon-Nykodym Derivative $\Lambda$ 는 다음과 같이 변경된다.

$$
\Lambda(X_{[0,T]}) = \frac{dQ}{dP} = \exp\left(-\int^T_0 \frac{\mu_2(X_t,t) - \mu_1(X_t, t)}{\sigma^2(X_t, t)} dX_t - \frac{1}{2} \int^T_0 \frac{\mu^2_2(X_t,t) - \mu^2_1(X_t, t)}{\sigma^2(X_t, t)} dt \right) \tag{1}
$$

이것이 Diffusion 모델의 Likelihood 가 된다. 이를 사용한 응용을 살펴보면 다음과 같다.

### Hypotheses Testing
어떤 신호가 White Noise 인지 그렇지 않으면 어떤 Diffusion을 가진 SDE 모델인지를 Test한다고 해보자.
White Noise는 $P$-Measurable 이라고 하고 (혹은 Null Hypothesis), 다른 하나는 $Q$-measurable Hypothesis 라고 하자. 그리고

|$H_0$ | Noise          | $dX_t = dB_t$ |
|------|:------|:------|
|$H_1$ | Noise + Signal | $dX_t = h(t)dt + dB_t$|

이 경우, $\mu_1(x,t)=0, \mu_2(x,t)=h(t), \sigma(x,t)=1$ 이다. 이를 위의 Diffusion에서의 Likelihood에 대입하면

$$
\Lambda(X)_{T} = \frac{dQ}{dP} = e^{\int^T_0 h(t) dX_t -\frac{1}{2}\int^T_0 h^2 (t) dt}
$$

위 값이 어떤 값 보다 크다 즉, $\Lambda(X)_{T} \geq k$ 이면 이는 두 프로세스 $H_0, H_1$ 이 유사하다는 의미 이므로 **Noise에 가깝다, 혹은 Noise가 많다** 라고 볼 수 있고 확률을 사용하여 다음과 같이 표시할 수도 있다.

$$
P(e^{\int^T_0 h(t) dX_t -\frac{1}{2}\int^T_0 h^2 (t) dt} \geq k) = \alpha
$$

k 보다 큰 값이 나올 확률이 $\alpha$ 이면 Noise 다, 라고 테스트 결과를 결정할 수 있다.

### Estimation in Ornstein-Uhlenbeck Model
다음의 friction parameter를 갖는 Ornsteign-Uhlenbeck Model 을 생각하자.

$$
dX_t = -\alpha X_t dt + \sigma dB_t
$$

이때 $X_t$에 대한 Probality는 $P_{\alpha}$, $\sigma B_t$의 Probablity는 $P_0$라고 할 때
이렇게 되면 방정식 (1)에 따라 Likelihood 함수는 다음과 같다.

$$
\Lambda(X)_{T} = \frac{dP_{\alpha}}{dP_0} = \exp\left(\int^T_0 \frac{-\alpha X_t}{\sigma^2} dX_t -\frac{1}{2}\int^T_0 \frac{\alpha^2 X^2_t}{\sigma^2} dt \right)
$$

$exp$ 함수 내부를 미분하여 최대값이 나오는 $\alpha$를 구하면 다음과 같다.

$$
\hat{\alpha} = \frac{\int^T_0 X_t dX_t}{\int^T_0 X^2_t dt}
$$

### Remark
Likelihood 를 논할 때 비교가 되는 두 모델은 동일한 Wiener Process를 공유하고 있어야 한다. 만일 양 모델이 서로 다른 모델을 공유하고 있다고 하면, 당연하게도 Radon-Dykodym Derivative 값이 Singular가 되어 Likelihood를 계산할 수 없게 된다. 

### Remark-2 : Simulated Annealing 
Stuart Geman and Chii-Ruey Hwang, " Diffusions for global optimization", SIAM. J. Control and Optimization, vol.24. No.5, pp1031-1043, Sept. 1986

$$
\begin{align}
dZ_u &= -\nabla U(Z_u) du + \sqrt{2T}dW_u \;\;\; &\text{Induced Probablity } P_x \\
dZ_u &= \sqrt{2T}dW_u \;\;\; &\text{Induced Probablity } Q_x 
\end{align}
$$

Then the Radon-Nykodym Derivation is 

$$
\frac{dP_x}{dQ_x}(Z_u) = \exp \left\{\int_{t}^{t+1} \frac{1}{2T(u)} \langle - \nabla \hat{U}(Z(u)), dZ(u) \rangle - \frac{1}{2} \int_{t}^{t+1} \frac{1}{2T(u)} | - \nabla \hat{U}(Z(u)) |^2 du \right\}
$$

이 결과는 위의 Ornstein-Uhlenbeck 프로세스에서의 결과와 동일하다.

