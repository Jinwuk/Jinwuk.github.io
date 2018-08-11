---
layout: post
title:  "Wiener Process Properties "
date:   2018-08-01 23:45:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
  - Kullback-Leibler Divergence
comments: true
---

* Table of Contents
{:toc}
다음의 Wiener Process 특성들을 정리한다.

| Process  | Expectation     |
|---|----|
| $e^{W_t}$ | $Ee^{W_t} = e^{\frac{1}{2}t}$ |
| $e^{\theta W_t}$ | $Ee^{\theta W_t} = e^{\frac{1}{2} \theta^2 t}$|
| $L_t = exp(-\frac{1}{2}\theta^2 t \pm \theta W_t)$ | $EL_t  = 1$|
| $S_t = S_0 \exp \left((\mu - \frac{1}{2} \sigma^2 ) t + \sigma W_t \right)$ | $ES_t = S_0 e^{\mu t}$|
| $W_t e^{\theta W_t}$ | $E(W_t e^{\theta W_t}) = \theta t e^{\frac{1}{2} \theta^2 t}$ |
| $W^2_t e^{\theta W_t}$ | $ E(W^2_t e^{\theta W_t})= (t + \theta^2 t^2) e^{\frac{1}{2} \theta^2 t}$ |

- $$E(W_s|W_t) = \frac{s}{t} W_s$$

- $$E(W_t | \mathcal{F}_s) = W_s$$
- $$E(W_t - t| \mathcal{F}_s) = W_s - s$$

- $$E(\exp(W_t - \frac{1}{2} t)| \mathcal{F}_s) = \exp(W_s - \frac{1}{2} s)$$
- $$E(e^{\theta W_t} | \mathcal{F}_s) = e^{\frac{1}{2}\theta^2 (t-s)}e^{\theta W_s}$$

- $$E(W_t e^{\theta W_t}| \mathcal{F}_s) = (W_s + \theta(t-s))e^{\frac{1}{2}\theta^2 (t-s)} e^{\theta W_s}$$
- $$E(W^2_t e^{\theta W_t}| \mathcal{F}_s) = ((t-s) + (W_s + \theta (t-s))^2)e^{\frac{1}{2}\theta^2 (t-s)} e^{\theta W_s}$$


## Fundamental Concept 
Let the pdf of $X_1 = W_1$ is 

$$
f(x) = \frac{1}{\sqrt{2 \pi} } \exp \left( -\frac{x^2}{2 } \right)
$$

Let the process of $Y_t = \sqrt{t} W_1 = \sqrt{t} X_t$ is

$$
f_X(x) = \frac{1}{\sqrt{2 \pi} t} \exp \left( -\frac{x^2}{2t } \right)
$$

## Fundamental Equation

$$
Ee^{W_t} = e^{\frac{1}{2}t}
$$

$$
Ee^{\theta W_t} = e^{\frac{1}{2} \theta^2 t}
$$

**Proof** 
since $\sigma^2 = t$

$$
\begin{align*}
E(e^{W_t}) &= \int_{-\infty}^{\infty} \frac{1}{\sqrt{2 \pi} t} \exp \left( -\frac{x^2}{2t} \right) e^{x} dx |_{x = W_t} \\ 
&= \int_{-\infty}^{\infty} \frac{1}{\sqrt{2 \pi} t} \exp \left( -\frac{x^2 -  2t x + t^2 - t^2 }{2t} \right) dx |_{x = W_t} \\  
&= \int_{-\infty}^{\infty} \frac{1}{\sqrt{2 \pi} t} \exp \left( -\frac{(x -  t)^2 -  t^2 }{2t} \right) dx |_{x = W_t} \\ 
&= e^{\frac{1}{2} t}\int_{-\infty}^{\infty} \frac{1}{\sqrt{2 \pi} t} \exp \left( -\frac{(x -  t)^2 }{2t} \right) dx |_{x = W_t} \\
&= e^{\frac{1}{2} t}
\end{align*}
$$

$$
\begin{align*}
E(e^{\theta W_t}) &= \int_{-\infty}^{\infty} \frac{1}{\sqrt{2 \pi} t} \exp \left( -\frac{x^2}{2t} \right) e^{\theta x} dx |_{x = W_t} \\ 
&= \int_{-\infty}^{\infty} \frac{1}{\sqrt{2 \pi} t} \exp \left( -\frac{x^2 -  2\theta t^2 x + \theta^2 t^2 - \theta^2 t^2 }{2t} \right) dx |_{x = W_t} \\  
&= \int_{-\infty}^{\infty} \frac{1}{\sqrt{2 \pi} t} \exp \left( -\frac{(x -  \theta t)^2 - \theta^2 t^2 }{2t} \right) dx |_{x = W_t} \\ 
&= e^{\frac{1}{2} \theta^2 t}\int_{-\infty}^{\infty} \frac{1}{\sqrt{2 \pi} t} \exp \left( -\frac{(x -  t)^2 }{2t} \right) dx |_{x = W_t} \\
&= e^{\frac{1}{2} \theta^2 t}
\end{align*}
$$

**Fast Proof** 
Remember $E(W_t) = 0$ and $(dW_t)^2 = dt $ so that

$$
\begin{align*}
e^{W_t} &= 1 + W_t + \frac{1}{2} W^2_t + o(W_t) \\
Ee^{W_t} &= 1 + EW_t + \frac{1}{2} EW^2_t + Eo(W_t) \\
&= 1 + \frac{1}{2} t + \frac{1}{4} t^2 + Eo(W_t) \\
&= e^{\frac{1}{2} t}
\end{align*}
$$

그리고

$$
\begin{align*}
e^{\theta W_t} &= 1 + \theta W_t + \frac{1}{2} \theta^2 W^2_t + \theta^n o(W_t) \\
Ee^{\theta W_t} &= 1 + \theta EW_t + \frac{1}{2} \theta^2 EW^2_t + \theta^n Eo(W_t) \\
&= 1 + \frac{1}{2} \theta^2 t + \frac{1}{4} \theta^4 t^2 + \theta^{2n} Eo(W_t) \\
&= e^{\frac{1}{2} \theta^2 t} 
\end{align*}
$$

즉, $W_t$의 제곱의 평균이 t 라는 것만 기억하면 파라미터 $\theta$ 가 있을 경우 $\theta W_t$는 당연히 $\theta$는 t에 대하여 제곱의 형태가 된다. 2의 배수승으로 $\theta$가 Taylor 급수 전개에서 살아남게 된다. 
이 방법이 더 기억하기에 좋다. 

이것을 기본으로 전개하자.

## Fundamental Operator $L_t$

다음 Operator는 Girsanov Theorem을 비롯하여 Geometrical SDE, Black Sholes등 매우 많은 SDE에서 많이 상요되고 나타나는 Operator이다

$$
\begin{align*}
L_t &= exp(-\frac{1}{2}\theta^2 t - \theta W_t) \\
L_t &= exp(-\frac{1}{2}\theta^2 t + \theta W_t)
\end{align*}
$$

$W_t$ 앞의 부호는 크게 문제가 되지 않는다. 이를 생각해 보면 다음과 같다. 
$\exp(-\frac{1}{2}\theta^2 t) = \left(Ee^{\pm\theta W_t } \right)^{-1}$  이기 때문에 이는 마치 $\left( Ee^{\pm\theta W_t } \right)^{-1} \cdot e^{\pm \theta W_t } = L_t$ 로 볼 수 있다. 

즉, **Normalize 된 $e^{\theta W_t}$ Process**  이다.
이것은 Linear Algebra 에서 흔히 볼 수 있는 Normalized Vector 형태이다. ($\frac{\vec{x}}{||x||}$)

따라서 

$$
EL_t = E\exp(-\frac{1}{2}\theta^2 t - \theta W_t) = 1   \tag{1}
$$

이다. Parameter가 있는 경우 (1) 의 Taylor 급수 전개에서 (-) 항은 $(-1)^{2n}$ 만 남기 때문이다.

$$
EL_t = E\exp(-\frac{1}{2}\theta^2 t - \theta W_t) = \exp(-\frac{1}{2}\theta^2 t) Ee^{- \theta W_t)} = \exp(-\frac{1}{2}\theta^2 t) \cdot \exp(\frac{1}{2}\theta^2 t)
$$

## Fundamental Operator $L_t$ with Drift $\mu$

Drift $\mu$ 가 있는 경우의 Fundamental Operator는 다음과 같다.

$$
L^{\mu}_t = \exp\left((\mu - \frac{1}{2} \sigma^2)t + \sigma W_t \right)
$$

Drift가 있는 경우 Fundamental Operator는 다음과 같이 생각할 수 있다.

$$
L^{\mu}_t = e^{\mu t} \left( Ee^{\sigma W_t} \right)^{-1} \cdot e^{\sigma W_t} \tag{2}
$$

즉, Normalized $e^{\sigma W_t}$ Process 에 $e^{\mu t}$가 곱해진 것이다. 
이는 선형 미분 방정식의 해 $e^{\mu t}$ 에 Normalized Exponential Process $e^{\theta W_t}$ 가 곱해진 형태이다. 

$L^{\mu}_t$ 프로세스를 가진 Process를 다음과 같이 정의하자

$$
S_t = S_0 \exp \left((\mu - \frac{1}{2} \sigma^2 ) t + \sigma W_t \right)
$$

이 프로세스의 평균 값은 그러므로 식 (2) 에서 

$$
ES_t = S_0 e^{\mu t}
$$

## Other Exponential Process

$$
\begin{align*}
EW_t e^{\theta W_t} &= t \theta e^{\frac{1}{2} \theta^2 t} \\
EW^2_t e^{\theta W_t} &= (t +\theta^2 t^2) e^{\frac{1}{2} \theta^2 t} \\
\end{align*}
$$

### Fast Proof
Using partial Derivatives to $\theta$

$$
EW_t e^{\theta W_t} = E(\frac{\partial}{\partial \theta} e^{\theta W_t}) = \frac{\partial}{\partial \theta} E( e^{\theta W_t}) = \frac{\partial}{\partial \theta} e^{\frac{1}{2} \theta^2 t} = t \theta e^{\frac{1}{2} \theta^2 t}
$$

$$
\begin{align*}
EW^2_t e^{\theta W_t} &= E(\frac{\partial^2}{\partial \theta^2}  e^{\theta W_t}) = \frac{\partial^2}{\partial \theta^2} E(e^{\theta W_t}) = \frac{\partial^2}{\partial \theta^2} e^{\frac{1}{2} \theta^2 t} = t \frac{\partial}{\partial \theta}\theta e^{\frac{1}{2} \theta^2 t} \\
&= t e^{\frac{1}{2} \theta^2 t} + t \theta \cdot t \theta e^{\frac{1}{2} \theta^2 t}
= (t + \theta^2 t^2 )e^{\frac{1}{2} \theta^2 t}
\end{align*}
$$

## Fundamental Properties of Martingale
### Basic Relation ships

$$
\begin{align*}
E(W_ s| W_t) &= \frac{s}{t}W_t \\
E(W_ t - W_s | \mathcal{F}_s ) &= E(W_ t - W_s ) = 0 \\
E((W_ t - W_s)W_s | \mathcal{F}_s ) &= E(W_t W_s | \mathcal{F}_s ) - E(W_s W_s | \mathcal{F}_s ) 
= s - s = 0  \\
E(e^{\theta (W_t - W_s)} | \mathcal{F}_s) &= E(e^{\theta (W_t - W_s)}) = E(e^{\theta W_{t - s}})
= e^{\frac{1}{2}\theta^2 (t-s)}
\end{align*}
$$

Since $(W_ t - W_s ) {\perp} \mathcal{F}_s$.

### Theorem 1 
$\{ W_t \}_{t \geq 0}$ 가 Brownian Motion 일때 다음은 Martingale 이다.
1. $\{ W_t \}_{t \geq 0}$ 은 Martingale 이다. 
2. $\{ W^2_t - t\}_{t \geq 0}$ 은 Martingale 이다.
3. $\{ \exp(W_t - \frac{1}{2} t)\}_{t \geq 0}$ 은 Martingale 이다.

이는 즉, 다음이다.

$$
\begin{align}
E(W_t | \mathcal{F}_s) &= W_s \\
E(W_t - t| \mathcal{F}_s) &= W_s - s\\
E(\exp(W_t - \frac{1}{2} t)| \mathcal{F}_s) &= \exp(W_s - \frac{1}{2} s) 
\end{align}
$$

### Corollary 1

$$
E(e^{\theta W_t} | \mathcal{F}_s) = e^{\frac{1}{2}\theta^2 (t-s)}e^{\theta W_s}
$$

**Fast Proof** 
먼저 $\mathcal{F}_s$ 와 무관한 Expectation 값을 찾고 이것과 Martingale 특성을 통해 문제를 푼다.
Theorem 1 의 3번쨰에서 

$$
\begin{align*}
E(e^{(\theta W_t - \frac{1}{2} \theta^2 t)}|\mathcal{F}_s ) &= e^{(\theta W_s - \frac{1}{2} \theta^2 s)} \\
e^{- \frac{1}{2} \theta^2 t} E(e^{\theta W_t }|\mathcal{F}_s ) &= e^{(\theta W_s - \frac{1}{2} \theta^2 s)} \\
E(e^{\theta W_t} | \mathcal{F}_s) &= e^{\frac{1}{2}\theta^2 (t-s)} e^{\theta W_s}
\end{align*}
$$

**Q.E.D**
Corollary 1 의 결과를 사용하면 다음을 알 수 있다.

$$
E(e^{\theta W_s} | \mathcal{F}_s) = e^{\frac{1}{2}\theta^2 (s-s)}e^{\theta W_s} = e^{\theta W_s}
$$

기본적으로 $X_t$가 Martingale 이면 $$ E(X_t \mid \mathcal{F}_s) $$ 는 Random Variable for $\mathcal{F}_s$ 가 존재해야 한다. 그래서 뒤 항에 $e^{\theta W_s}$ 가 존재한다. (그래서 Martingale. 같은 형식의 R.V. 가 평균 값) 그래서 이렇게 생각해야 한다. $$E(X_t \mid \mathcal{F}_s) = X_s $$ 즉, Theorem 1의 첫번쨰 방정식이다. 

이 특징과 Martingale Basic Relationship을 사용하면 다음과 같이 Corollary 1을 다르게 풀 수 있는 방법이 있다.

**Alternative Proof of Colloray 2**
$W_t - W_s \perp W_s$ 이므로

$$
E(e^{\theta (W_t - W_s) + W_s} | \mathcal{F}_s) = E(e^{\theta (W_t - W_s)}) E(e^{W_s}|\mathcal{F}_s) = E(e^{\theta W_{t - s}}) e^{\theta W_s} = e^{\frac{1}{2}\theta^2 (t-s)}e^{\theta W_s}
$$

**Q.E.D**

### Corollary 2

$$
E(W_t e^{\theta W_t}| \mathcal{F}_s) = (W_s + \theta(t-s))e^{\frac{1}{2}\theta^2 (t-s)} e^{\theta W_s}
$$

**Fast proof** 

$$
\begin{align*}
E(W_t e^{\theta W_t}| \mathcal{F}_s) &= E(\frac{\partial}{\partial \theta} e^{\theta W_t} | \mathcal{F}_s) = \frac{\partial}{\partial \theta } E(e^{\theta W_t}|\mathcal{F}_s) = \frac{\partial}{\partial \theta} e^{\frac{1}{2} \theta^2(t-s)}e^{\theta W_s} \\
&= \left( \theta (t-s) + W_s \right) e^{\frac{1}{2} \theta^2(t-s)}e^{\theta W_s}
\end{align*}
$$

**Q.E.D.** 

### Corollary 3

$$
E(W^2_t e^{\theta W_t}| \mathcal{F}_s) = ((t-s) + (W_s + \theta (t-s))^2)e^{\frac{1}{2}\theta^2 (t-s)} e^{\theta W_s}
$$

**Fast proof** 

$$
\begin{align*}
E(W^2_t e^{\theta W_t}| \mathcal{F}_s) &= E(\frac{\partial^2}{\partial \theta^2} e^{\theta W_t} | \mathcal{F}_s) = \frac{\partial^2}{\partial \theta^2} E(e^{\theta W_t}|\mathcal{F}_s) = \frac{\partial^2}{\partial \theta^2} e^{\frac{1}{2} \theta^2(t-s)}e^{\theta W_s} \\
&= \frac{\partial}{\partial \theta}\left( \theta (t-s) + W_s \right) e^{\frac{1}{2} \theta^2(t-s)}e^{\theta W_s} \\
&= \left((t-s) + (W_s + \theta (t-s))^2 \right)e^{\frac{1}{2} \theta^2(t-s)}e^{\theta W_s}
\end{align*}
$$

**Q.E.D.** 


