---
layout: post
title:  "Ito Formula - Solution of Basic SDE "
date:   2018-08-12 01:45:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
  - Geometrical SDE
comments: true
---

* Table of Contents
{:toc}

This article is a brief of the fundamental concept of Ito calculus, thus this article is written in the Korean language.  Especially, it deals with the way of the solution about the geometrical stochastic differential equation with the various aspect.

## Simple Fundamental Case

다음을 증명해 보자.

$$
\int_0^t W_s dW_s= \frac{1}{2}W^2_t - \frac{1}{2} t
$$

Classical 한 증명도 있지만 빠른 증명을 생각해보자

Let $f(t, x) = \frac{1}{2} x^2$ 의 경우 즉, 굉장히 일반적인 Quadratic한 경우를 생각해 보면
여기에 $dX_t = dW_t$ 라 놓으면 Ito Differential 에 의해 

$$
df = \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} dX_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} (dX_t)^2
$$

여기서 $\partial_t f = 0, \; \partial^2_{x^2} f = 1$ 이므로 

$$
df = x dW_t + \frac{1}{2} dt
$$

그런데 가정에서 $dX_t = dW_t$ 이므로 $x = W_t$ 대입하고 정리하면 

$$
\begin{align*}
df &= W_t dW_t + \frac{1}{2} dt \\
W_t dW_t &= df - \frac{1}{2} dt \\
\int_0^t W_s dW_s &= \int_0^x df - \frac{1}{2} \int_0^t ds \\
\int_0^t W_s dW_s &=  \frac{1}{2} x^2|_{x=W_t} - \frac{1}{2} t
\end{align*}
$$

따라서

$$
\int_0^t W_s dW_s =  \frac{1}{2} W^2_t - \frac{1}{2} t
$$

## Deduction of Ito Differential Equation
Set the Following Fundamental SDE

$$
dX_t = a(x,t)dt + \sigma(x,t)dW_t
$$

Then, since $(dX_t)^2 = \sigma^2(x,t) dt$ 

$$
\begin{align*}
df &= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} dX_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} (dX_t)^2 \\
&= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} (a(x,t)dt + \sigma(x,t)dW_t) + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} (dX_t)^2 \\
&= \left(\frac{\partial f}{\partial t} + a(x,t)\frac{\partial f}{\partial x} \right)dt + \sigma(x,t)\frac{\partial f}{\partial x}dW_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \sigma^2(x,t) dt \\
&= \left(\frac{\partial f}{\partial t} + a(x,t)\frac{\partial f}{\partial x} + \frac{1}{2} \sigma^2(x,t) \frac{\partial^2 f}{\partial x^2} \right)dt + \sigma(x,t)\frac{\partial f}{\partial x}dW_t
\end{align*}
$$

## Geometrical Brown motion
Consider the following SDE

$$
dS_t = \mu S_t dt + \sigma S_t dW_t
$$

이러한 SDE를 만족하는 프로세스 $S_t$를 기하 브라운 운동이라고 한다. 이를 풀기위하여는 ITo 미분방정식의 해법을 사용해야 한다.

1. $$S_t = f(t, x) \mid_{x = W_t}$$ 로 놓고 편미분 방정식을 풀듯, Ito 미방을 세우고 푼다.
2. 즉, **Simple Fundamental Case** 에서 나타났듯이, $f(t,x)$에 대한 Ito 미분

$$
df = \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} dX_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} (dX_t)^2
$$

을 놓고 $df = dS_t$ 로 생각하면 된다. 그리고 $x=W_t$ 로 놓았기 때문에 $dx_t = dW_t$ 이다. 그러므로

$$
\begin{align*}
dS_t &= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} dX_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} (dX_t)^2 \\
dS_t &= \left( \frac{\partial f}{\partial t} + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \right) dt + \frac{\partial f}{\partial x} dW_t 
\end{align*}
$$

그러므로

$$
\begin{align}
\mu S_t &= \frac{\partial f}{\partial t} + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \\
\sigma S_t &= \frac{\partial f}{\partial x} 
\end{align}
$$

앞에서 $S_t = f(x,t)\mid_{x=W_t}$ 라고 했으므로 위 방정식은 보다 알기 쉬운 형태가 된다.

$$
\begin{align}
\frac{\partial f}{\partial t} (t,x) + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} (t,x)&= \mu f(t,x) \tag{1}\\
\frac{\partial f}{\partial x}(t,x)  &= \sigma f(t,x) \label{eq:01} \tag{2}
\end{align}
$$

식 ($\ref{eq:01}$) 에서 $f(x,t) = h(t)e^{\sigma x}$ 로 놓으면 

$$
\frac{\partial f}{\partial t} + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} = h'(t) e^{\sigma x} + \frac{1}{2} h(t) \sigma^2 e^{\sigma x} = \mu h(t)e^{\sigma x}
$$

에서

$$
h'(t) = (\mu - \frac{1}{2} \sigma^2)h(t) \Rightarrow h(t) = C e^{(\mu - \frac{1}{2} \sigma^2)t} 
$$

그러므로 $f(x,t) = C e^{(\mu - \frac{1}{2} \sigma^2)t + \sigma x}$ 이므로 

$$
S_t = S_0 e^{(\mu - \frac{1}{2} \sigma^2)t + \sigma W_t}
$$

이 프로세스는 Martingale 이며 평균은

$$
ES_t = S_0 e^{\mu t} \cdot e^{-\frac{1}{2} \sigma^2 t} Ee^{\sigma W_t} =  S_0 e^{\mu t} ( Ee^{\sigma W_t})^{-1}  Ee^{\sigma W_t} = S_0 e^{\mu t}
$$

이다. 

## Ito Integral As Martingale
### Theorem 1 [Ito Integral is Martingale]

$$\{W_t \}_{t \geq 0}$$ is $$(\rm{P}, \{\mathcal{F}_t \}_{t \geq 0})$$ - Wiener process. For each $t$, $f(t,w)$ is a $\mathcal{F}_t$ measurable random variable, and

$$
E(f^2 (t,w)) < \infty
$$

, then the stochastic process 

$$
M_t = \int_0^t f(s,w) dW_s
$$

is a **Martingale.** 

위 정리는 사실로서 받아들이자 (다른 text들에 부지기수로 증명이 나와 있다.)

재미있는 것은 결국 $M_0 = \int_0^0 f(s,w) dW_s = 0$ 이기 때문에 $EM_0 = 0$ 이고 Martingale이기 때문에 $EM_t = EM_0 = 0$ 이다.

이 사실을 사용하여 위 Geoemtrical SDE의 평균값을 다시 계산해 보면 

$$
dS_t = \mu S_t dt + \sigma S_t dW_t 
$$

에서

$$
S_t - S_0 = \int^t_0 \mu S_t dt + \int^t_0 S_t dW_t
$$

이므로 Ito Integral의 Martingale 성질에서 $\int^t_0 S_t dW_t = 0$ 이므로 

$$
\begin{align*}
ES_t &= S_0 + \int^t_0 \mu S_t dt \\
EdS_t &= \mu S_t dt \\
ES_t &= S_0 e^{\mu t}
\end{align*}
$$

### Notice (of Ito integral as Martingale)
그러므로 편미분 방정식 중에서 $dt$ 에 대한 PDF solution을 찾고 이것을 이용하여 Martingale 특성을 갖도록 하는 $M_t = \int_0^t f(s,w) dW_s $ 해를 구하면 SDE의 해를 구하는 것이 된다. (생각보다는 만만하지 않다.)
- 이를 가능하게 하려면 **Girsanov Theorem** 이 필요하다.

예를 들어

$$
EdS_t = (\frac{\partial f}{\partial t} + \frac{1}{2} \frac{\partial^2 f}{\partial x^2})dt = \mu S_t dt
$$

이것의 의미는 
$$
f(t,x)\mid_{x=W_t} = e^{\mu t}g(t,x)\mid_{x=W_t} = e^{\mu t}\bar{g}(t) E(\bar{h}(W_t))
$$
가 존재하여 다음을 만족시킨다는 의미이다.

$$
\frac{\partial f}{\partial x} = \sigma f
$$

하지만, 이를 위 예제에 대입하여 생각해 보면 결국 풀수는 있으나 일반적인 방법론이 되기는 어렵다.
오히려, 앞에서 소개한 방법에 의해 $\frac{\partial f}{\partial x} = \sigma f$ 를 푸는 것은 간단하므로 이를 사용하여 Stochastoc Process를 하나 얻고 즉, $$f(x,t)\mid_{x=W_t} = h(t)e^{\sigma x} \mid_{x=W_t}$$ 이것이 Maringale이 되게 하는 $h(t)$를 구하는 것, 즉, Girsanov Theorem으로 접근하는 것이 더욱 일반적이다. 

간단히 생각해보면 

$$
E h(t)e^{\sigma W_t} = h(t) e^{\frac{1}{2} \sigma^2 t} = e^{\mu t}
$$

에서 $E(\bar{h}(W_t))=1$ 되도록 하면 $t$ 에 대한 방정식이 되므로 일반적인 편미분 방정식의 해법 (상미분 방정식 만들기)이 된다. 다시말해 $h(t) = e^{\mu t}e^{-\frac{1}{2} \sigma^2 t}$, 되게 하면 해결이 된다.

- 첫번째 편미분항의 계산

$$
\frac{\partial f}{\partial t} + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} = \left((\mu - \frac{1}{2} \sigma^2) + \frac{1}{2} \sigma^2 \right) e^{(\mu - \frac{1}{2} \sigma^2)t+\sigma x}
= \mu S_t
$$

- 두번째 편미분항의 계산

$$
\frac{\partial f}{\partial x} = \sigma e^{(\mu - \frac{1}{2} \sigma^2)t+\sigma x} = \sigma S_t
$$

정리하면
- $dW_t$ 에 대한 상미분 방정식을 푼다. ($W_t$를 $x$로 보고)
- Girsanov Theorem등에 의해 이를 Martingale로 만들 수 있는 보조 함수를 구한다.
- $dt$ 에 대한 미분 방정식 해를 여기에 대입하여 최종 해를 구한다. 

Feynmann-Kac 방정식도 이렇게 해를 구할 수 있을 것이다. 

## Martingale 특성을 사용한 Geometrical SDE 의 더 빠른 해석

앞에서 $EdS_t = \mu S_t dt$ 라고 놓았다. 그렇다면,$E \frac{1}{S_t} dS_t = \mu dt$ 에서 $ln(S_t) = \mu t + C_0$ 이다. 좌항을 보았을때, 결국 **$S_t$ 의 log가 나온다는 의미**이므로 **$f(x) = \ln(x)$** 를 놓고 이를 사용하여 SDE를 풀어보자. 여기서 $x$는 결국 $X_t$ (다시말해 $S_t$ 인) 통짜로 stochastic Process로 간주된다.

- Let the Geometrical SDE

$$
dX_t = \mu X_t dt + \sigma X_t dW_t
$$

- $f(x) = \ln(x)$ 에 대한 1, 2차 미분

$$
\frac{\partial f}{\partial x} = \frac{1}{x}, \;\; \frac{\partial^2 f}{\partial x^2} = - \frac{1}{x^2}, \;\; \frac{\partial f}{\partial t} = 0
$$

- $f(X_t)$ ($S_t$로 $X_t$를 놓아도 된다.) 에 대한 Ito SDE

$$
\begin{align*}
df(X_t) = d(\ln(X_t)) &= \frac{\partial f}{\partial x} dX_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} (dX_t)^2 \\
&= \frac{1}{X_t} \left( \mu X_t dt + \sigma X_t dW_t \right) - \frac{1}{2} \frac{1}{X^2_t} \sigma^2 X^2_t dt \\
&= \left( \mu - \frac{1}{2} \sigma^2 \right)dt + \sigma dW_t 
\end{align*}
$$

그러므로 

$$
\int^t_0  d(\ln(X_t)) = \int^t_0 \left( \mu - \frac{1}{2} \sigma^2 \right)dt + \int^t_0 \sigma dW_t 
$$

$$
X_t = X_0 e^{( \mu - \frac{1}{2} \sigma^2 )t + \sigma W_t}
$$

## Langevine Equation의 경우 
다음의 SDE를 생각해 보자

$$
dS_t = -\alpha S_t dt + \sigma dW_t
$$

### 1. 정통적인 방법 ($S_t = f(t,x)|_{x = W_t}, \; dx = dW_t$)
Let $S_t = f(t,x)|_{x = W_t}$ 그리고 $x = W_t$ 에서 $dX_t = dW_t$ 라 놓고 Ito SDE를 전개하면 

$$
\begin{align*}
df &= \frac{\partial f}{\partial t} + \frac{\partial f}{\partial x}dX_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} dt \\
&= (\frac{\partial f}{\partial t} + \frac{1}{2} \frac{\partial^2 f}{\partial x^2}  )dt + \frac{\partial f}{\partial x} dW_t = -\alpha S_t dt + \sigma dW_t
\end{align*}
$$

일단, 쉽게 구해지는 $dW_t$ 항 부터 보면

$$
\frac{\partial f}{\partial x} = \sigma \rightarrow f=h(t)(C_0 + \int^x_0 h^{-1}(t) \sigma dx)
$$

적분항 내에 $h^{-1}(t)$가 있어애 원래의 미분 방정식이 나온다. 이것을 $dt$ 에 놓고 구하기 위해서

$$
\frac{\partial f}{\partial t} + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} = -\alpha f = C_0 h'(t)\;\;  \because \frac{1}{2} \frac{\partial^2 f}{\partial x^2} = 0
$$

$$
-\alpha C_0 h(t) + \sigma x = C_0 h'(t)
$$

$x$가 임의의 값일 때도 미분에서는 상관 없기 때문에 ($\partial_x f = \sigma, \partial^2_{x^2} f  = 0$) $x=0$ 이라 놓고 풀면 

$$
-\alpha C_0 h(t)= C_0 h'(t), \;\; h(t) = e^{-\alpha t}
$$

따라서 Langevine 방정식의 해는

$$
S_t = e^{-\alpha t}(C_0 + \int^t_0 \sigma e^{\alpha s}  dW_s)
$$

### 2. Alternative Solution 

$$
EdS_t = -\alpha S_t dt 
$$

에서 $\Psi(t) = e^{-\alpha t}$ 라 볼 수 있다. 이때 $S_t = \Psi(t)X_t$ 라고 하면 

$$
dS_t = -\alpha e^{-\alpha t} X_t dt + e^{-\alpha t} dX_t  \tag{3}
$$

가 된다. 이것이 동일한 Langevine 방정식이 되려면 $dX_t = e^{\alpha t} \sigma dW_t$ 이어야 한다. (앞의 $dt$ 항의 경우 이미 $S_t = \Psi(t)X_t$ 에서 $X_t = e^{\alpha t}S_t$ 로서 조건이 만족된다. 바로 이 식을 만족하는 미분 방정식에서 출발하였기 때문이다.)
그런데, 이 방정식은 간단한 Only Wiener Process  이므로 양변에 적분을 취하면 

$$
X_t = C_0 + \int^x_0 e^{\alpha t} \sigma dW_t
$$

이를 사용하면

$$
S_t = e^{-\alpha t}(C_0 + \int^t_0 e^{\alpha s} \sigma dW_s)
$$

## Notice 2
### 정통적인 방법의 정리
1. $$S_t = f(t,x)\mid_{x=W_t}$$,  $dX_t = dW_t$ 로 놓고 Ito Differential Equation을 전개한다.
2. $dW_t$에 대한 미분 방정식  $\frac{\partial f}{\partial x} = h(x)$을 풀어서 이를 기반으로 Ito 미분방정식을 푼다.

### 또 다른 방법
1. 문제로 주어진 SDE에서 $EdS_t = \mu(t,x)dt$ 를 기반으로 1차 미분방정식을 푼다.
2. Transition 함수 $\Psi(t)$ 를 구하고 $$S_t = f(t,x)\mid_{x = W-t}=\Psi(t)h(x,t)\mid_{x= W-t}$$ 로 놓고 x에 대한 미분방정식을 푼다.
   - $h(x)$ 가 아닌 $h(x,t)$인 이유는 $\frac{\partial f}{\partial t}$ 가 존재하여 $dt$ 에 대하여 $\frac{\partial f}{\partial t} + \frac{1}{2} \frac{\partial^2 f}{\partial x^2}$ 를 전개해야 하기 때문이다. 이는 앞에서 구한 Transition 함수로 모두  Cover 되지 않기 때문이다.

#### Geometrical SDE를 두번째 방법으로 푸는 경우
동일하게 $\Psi(t) = e^{\mu t}$ 이 경우 $S_t = f(x,t) = \Psi(t)g(x,t)$ 로 볼 수 있다.
먼저 $dW_t$ 항에 대해서 생각해보면 

$$
\frac{\partial f}{\partial x} = \sigma S_t = \sigma f(x,t) =  \sigma  \Psi(t)g(x,t) = \Psi(t
) \frac{\partial g}{\partial x}(x,t)
$$

$t=0$ 에 대한 해를 구하면 $g(0, x) = C_0 e^{\sigma x}$ 로 볼 수 있다. 특별히 $C_0 = 1$ 로 놓고 $g(0,x)=h(t)e^{\sigma x}$로 놓으면 

$$
\frac{\partial f}{\partial t} + \frac{1}{2}\frac{\partial^2 f}{\partial x^2} = \mu e^{\mu t}  e^{\sigma x} h(t) +  e^{\mu t}e^{\sigma x} h'(t) + \frac{1}{2} \sigma^2 e^{\mu t}e^{\sigma x} h(t) = \mu e^{\mu t} e^{\sigma x} h(t)
$$

따라서

$$
h(t) = e^{-\frac{1}{2} \sigma^2 t}
$$

그러므로 최종 솔루션은

$$
S_t = S_0 e^{(\mu - \frac{1}{2}\sigma^2)t + \sigma W_t}
$$

생각해보면 결국 정통적인 방법으로 푼 것과 같은 것이다.
따라서, 일단, 일반적인 방법은 정통적인 방법으로 Solution을 구하는 것이며 좀 더 단순한 형태나 특이한 형태가 발견될 시에 다른 변형 방법을 도입하는 것이 좋다.


