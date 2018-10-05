---
layout: post
title:  "Mathematical Analysis of Quantization Parameter in HEVC"
date:   2018-10-05 19:40:00 +0900
categories: [Multimedia and Programming, Video Processing]
tags:
  - HEVC
  - Qunatization
comments: true
---

The mathematical analysis provided by this article is conducted for the development of a novel video compression based on a neural network.
We illustrate the quantization method represented in the standard draft of HEVC video coding with mathematical equations.
In addition, we provides simple python codes to verify the represented equations in this article comparing to the HEVC standard. 


## 기본 양자화 방정식 

비디오 코덱에서는 기본적으로 다음과 같은 방식으로 Quantization을 수행한다. 

$$
Q(\mathcal{X}, q) = \left[ \frac{1}{q^{s}} \mathcal{X} \right] \approx \left[ \frac{1}{q^{s}} \mathcal{X} \times 2^{qbits} \right] \gg qbits

\tag{1}
$$

여기서 $bits$는 14이다. 

그런데, 직접 정수 나눗셈을 수행하는 것이 아니라,  Shift 연산을 통해 정수 나눗셈을 필요한 정확도를 가지면서 수행하는 것이 비디오 코덱의 기본이다. 이를 위해 기본적인 Quantization  범위를 살펴보면 다음과 같다. 

|qp    | 0   | 1   | 2   | 3   | 4 | 5   | 6  |
|---   |---  |---  |---  |---  |---|---  |--- |
|$q^{s}$|0.625|0.703|0.797|0.891|1.0|1.125|1.25|

이를 수식으로 나타내면 다음과 같다고 하면. 

$$
q^s = 0.625 \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor + k \cdot (q \mod 6)}
\tag{2}
$$

이떄, 비례상수 $k$를 알아보기 위해 위 식을 정리하면 다음과 같은 방정식이 유도된다.  만일 $m = (q \mod 6)$ 이라 하고 $m$ 값일 때의 Quantization Step을 $q_m^s$ 라 하면 

$$
\begin{aligned}
q_m^s &= 0.625 \cdot 2^{\left( \left \lfloor \frac{q}{6} \right \rfloor + k \cdot m \right)} \\

\frac{q_m^s}{0.625} &= 2^{\left( \left \lfloor \frac{q}{6} \right \rfloor + k \cdot m \right)} \\

\log_2 \frac{q_m^s}{0.625} &= \left \lfloor \frac{q}{6} \right \rfloor + k \cdot m \\

k &= \frac{1}{m} \cdot \left( \log_2 \frac{q_m^s}{0.625} - \left \lfloor \frac{q}{6} \right \rfloor \right)

\end{aligned}
\tag{3}
$$

위 표와 같은 결과를 얻기 위해서 $q \in \mathbf{Z}(0, 6)$ 인 경우를 알아보면 $\left \lfloor \frac{q}{6} \right \rfloor = 0$ 이므로,  이것의 Least mean square error를 최소화 하는 $\bar {k} = \frac{1}{N} \sum_{m=1}^N k_m$를 알아본다. 

다음과 같은 Python 프로그램을 통해 결과를 알아본다.

~~~python
npA = np.array([ 0.625,  0.703,  0.797,  0.891,  1.   ,  1.125])
npQA = npA[1:6]
npK = np.log2(npQA/0.625) * 1/np.array(list(range(1, 6)))

>>>sum(npK)/5
0.17093414099804752
~~~

|m     | 1   | 2   | 3   | 4   | 5   |Average|
|---   |---  |---  |---  |---  |---  |---  |
| $k$ |0.1696685|0.17536177|0.17052308|0.16951798|0.16959938|0.17093414|

식 (2)를  식(1)에 대입하여 정리하면

$$
\begin{aligned}
Q(\mathcal{X}, q) &\approx \left[ \frac{1}{0.625 \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor + k \cdot m}} \mathcal{X} \times 2^{qbits} \right] \gg qbits \\

&= \left[ \frac{8}{5} \cdot 2^{-\left( \left \lfloor \frac{q}{6} \right \rfloor + k \cdot m \right)} \mathcal{X} \times 2^{qbits} \right] \gg qbits \\

&= \left[ \frac{8}{5} \cdot 2^{qbits - k \cdot m} \mathcal{X} \times 2^{- \left \lfloor \frac{q}{6} \right \rfloor} \right] \gg qbits \\

&\approx \left[ \frac{8}{5} \cdot 2^{qbits - \left( \log_2 \frac{q_m^s}{0.625} - \left \lfloor \frac{q}{6} \right \rfloor \right)} \mathcal{X} \right] \gg (qbits + \left \lfloor \frac{q}{6} \right \rfloor) \\

&= \left[ \left( \frac{8}{5} \cdot 2^{qbits - \log_2 \frac{q_m^s}{0.625}} \right) 2^{\left \lfloor \frac{q}{6} \right \rfloor } \mathcal{X} \right] \gg (qbits + \left \lfloor \frac{q}{6} \right \rfloor) \\

&= \left[ \left( \frac{8}{5} \cdot 2^{- \log_2 \frac{q_m^s}{0.625}} \cdot 2^{qbits} \right)  \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor } \mathcal{X} \right] \gg (qbits + \left \lfloor \frac{q}{6} \right \rfloor) \\

&= \left[ \left( \frac{8}{5} \cdot \frac{0.625}{q_m^s} \cdot 2^{qbits} \right) \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor } \mathcal{X} \right] \gg (qbits + \left \lfloor \frac{q}{6} \right \rfloor) \\

&= \left[ \left( \frac{1}{q_m^s} \cdot 2^{qbits} \right) \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor } \mathcal{X} \right] \gg (qbits + \left \lfloor \frac{q}{6} \right \rfloor)
\end{aligned}
\tag{4}
$$

식 (4)에서 $q_m^s$ 의 값은 $m = (q \mod 6)$ 에 따라 표 1 과 같으므로 $\left( \frac{1}{q_m^s} \cdot 2^{qbits} \right)$ 를  $m \in \mathbf{Z}[0,5]$ 의 값으로 다음 Python 코드로 간단히 계산하면 

~~~
>>>
>>> (1/npA[0:5]) * 16384
array([ 26214.4, 23305.83214794,  20557.08908407,  18388.32772166,
        16384. , 14563.55555556 ])
~~~

이를 반올림 하여 정수화 시킨 값과 HEVC의 Quant Scale 값을 비교해 보면 다음과 같다.

|m      | 0   | 1   | 2   | 3   | 4   | 5   |
|---    |---  |---  |---  |---  |---  |---  |
| Eval  |26214|23306|20557|18388|16384|14564|
| HEVC  |26214|23302|20560|18396|16384|14564|

여기에 입력 데이터의 비트심도 (8/10 bit)와 변환 부호화 크기에 따른 변환 부호화의 스케일을 고려하여 5 비트의 추가 Shift가 필요하다.  이를 고려하면 식 (4)는 다음과 같이 쓸 수 있다. 

$$
\begin{aligned}
Q(\mathcal{X}, q) &\approx \left[ \left( \frac{1}{q_m^s} \cdot 2^{qbits} \right) \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor } \cdot 2^5 \cdot \mathcal{X} \right] \gg (qbits + \left \lfloor \frac{q}{6} \right \rfloor + 5) \\

&= \left[ \left( \frac{1}{q_m^s} \cdot 2^{qbits} \right) \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor } \cdot \bar{\mathcal{X}} \right] \gg (qbits + \left \lfloor \frac{q}{6} \right \rfloor + 5)
\end{aligned}
$$

따라서 이 값의 반올림을 한다고 가정하면  다음과 같아야 한다.

$$
\begin{aligned}
Q(\mathcal{X}, q) &\approx \left[ \frac{1}{q_m^s} \cdot 2^{qbits + \left \lfloor \frac{q}{6} \right \rfloor} \cdot \bar{\mathcal{X}} \right] \gg (qbits + \left \lfloor \frac{q}{6} \right \rfloor + 5) \\

&= \left \lfloor \frac{1}{q_m^s} \cdot 2^{qbits + \left \lfloor \frac{q}{6} \right \rfloor} \cdot \bar{\mathcal{X}} + f \right \rfloor \gg (qbits + \left \lfloor \frac{q}{6} \right \rfloor + 5)
\end{aligned}
$$

일반적인 반 올림이 되기 위해서는 $f$ 의 값이 다음과 같아야 한다. 
- 외부에서 수행되는 나눗셈 때문에 $2^{qbits + \left \lfloor \frac{q}{6} \right \rfloor + 5}$ 이 곱해져야 한다.

$$
f = \frac{1}{2} q_m^s \cdot 2^{qbits + \left \lfloor \frac{q}{6} \right \rfloor + 5}
$$

따라서,  Scale Factor $2^{qbits + \left \lfloor \frac{q}{6} \right \rfloor + 5}$ 를 생각하지 않는다면 $f$ 는 다음의 범위를 가지는 것이 정상이다. 

$$
0.3125 \leq \frac{1}{2} q_m^s \leq 0.5625
$$

HEVC에서 $f$의 값은 Intra의 경우 $f = \frac{1}{3} \cdot 2^{qbits + \left \lfloor \frac{q}{6} \right \rfloor + 5}$ Inter의 경우 $f = \frac{1}{6} \cdot 2^{qbits + \left \lfloor \frac{q}{6} \right \rfloor + 5}$ 이다. 그러므로 HEVC에서의 반올림 팩터는  Intra에서 $\frac{1}{3} = 0.3333 \cdots$,  Inter에서는 $\frac{1}{6} = 0.16666 \cdots$ 이다. 특히 Inter의 경우에는 지나치게 낮아서 제대로 반올림이 되기에는 낮은 값이다. 이는 상당히 높은 값을 가져야만 반올림되어 값이 수정됨을 의미한다.  이런 경우 다음과 같은 경우가 발생할 수 있다.

- $q_2 = q_1 + 6$ 이고  $f_{q} = f_0  \cdot 2^{qbits + \left \lfloor \frac{q}{6} \right \rfloor + 5}$ 이라 하면 

$$
\begin{aligned}
f_{q_1} &= f_0  \cdot 2^{qbits + \left \lfloor \frac{q_1}{6} \right \rfloor + 5} \\

f_{q_2} &= \cdot f_0  \cdot 2^{qbits + \left \lfloor \frac{q_2}{6} \right \rfloor + 5} = 2 \cdot f_0  \cdot 2^{qbits + \left \lfloor \frac{q_1}{6} \right \rfloor + 5} = 2 f_{q_1} 
\end{aligned}
$$

$$
\begin{aligned}
Q(\mathcal{X}, q_1) &\approx \left \lfloor \frac{1}{q_m^s} \cdot 2^{qbits + \left \lfloor \frac{q_1}{6} \right \rfloor} \cdot \bar{\mathcal{X}} + f_{q_1} \right \rfloor \gg (qbits + \left \lfloor \frac{q_1}{6} \right \rfloor + 5) = \lfloor A \rfloor \gg B\\

Q(\mathcal{X}, q_2) &\approx \left \lfloor \frac{1}{q_m^s} \cdot 2^{qbits + \left \lfloor \frac{q_2}{6} \right \rfloor} \cdot \bar{\mathcal{X}} + f_{q_2} \right \rfloor \gg (qbits + \left \lfloor \frac{q_2}{6} \right \rfloor + 5) \\ 

&=\left \lfloor \frac{1}{q_m^s} \cdot 2^{qbits + \left \lfloor \frac{q_1 + 6}{6} \right \rfloor} \cdot \bar{\mathcal{X}} + f_{q_2} \right \rfloor \gg (qbits + \left \lfloor \frac{q_1 + 6}{6} \right \rfloor + 5) \\

&=\left \lfloor 2 \cdot \frac{1}{q_m^s} \cdot 2^{qbits + \left \lfloor \frac{q_1}{6} \right \rfloor} \cdot \bar{\mathcal{X}} + 2 f_{q_1}  \right \rfloor \gg (qbits + \left \lfloor \frac{q_1}{6} \right \rfloor + 5 + 1 ) = \lfloor 2 A \rfloor \gg (B + 1)
\end{aligned}
$$



## Quantization 과 Gauss Function

식 (1)은 근사 방정식이다. 그런데, 이것이 등식이 되기 위한 조건을 생각해 보자. 

$$
\begin{aligned}
\left[ \frac{1}{q^{s}} \mathcal{X} \right]  &= \left[ \frac{1}{q^{s}} \mathcal{X} \cdot 2^{qbits} \cdot 2^{-qbits}  \right] \\

&= \left[ \frac{8}{5} \cdot 2^{\left( qbits - \left \lfloor \frac{q}{6} \right \rfloor - k \cdot m \right)} \mathcal{X} \cdot  2^{-qbits} \right] \\

&= \left[ \frac{1}{10} \cdot 2^{\left( qbits - \left \lfloor \frac{q}{6} \right \rfloor + 4 - k \cdot m \right)} \mathcal{X} \cdot  2^{-qbits} \right]

\end{aligned}
\tag{5}
$$

정수 $L(q) = qbits - \left \lfloor \frac{q}{6} \right \rfloor+ 4 = 18 - \left \lfloor \frac{q}{6} \right \rfloor \in \mathbf{Z}$  를 정의하자. 

이 경우 방정식 (5)는 다음과 같다.

$$
\begin{aligned}
\left[ \frac{1}{q^{s}} \mathcal{X} \right]  

&= \left[ \frac{2^{- k \cdot m}}{10} \cdot \mathcal{X} \cdot 2^{L(q)}  \cdot  2^{-qbits} \right] \\

&= \left[ \frac{2^{- k \cdot m}}{10} \cdot \mathcal{X} \cdot 2^{10 + 8 - \left \lfloor \frac{q}{6} \right \rfloor}  \cdot  2^{-qbits} \right]

\end{aligned}
\tag{6}
$$

식 (6) 에서 $\left \lfloor \frac{q}{6} \right \rfloor \in \mathbf{Z}[0, 8]$ 이므로 $8 - \left \lfloor \frac{q}{6} \right \rfloor = 2^p$ where $ p \in \mathbf{Z}[0, 8]$ 그리고   $km \in \mathbf{R}[0, 1)$ 이므로 

따라서  다음을 만족 시킬 수 있는 정수 $\lambda \in \mathbf{Z}$가 존재한다고 하면, 

$$
\frac{2^{- k \cdot m}}{10} \cdot \mathcal{X} \cdot 2^{10} = 2^{\lambda}
\tag{7}
$$

그리고, $\lambda + p \geq qbits \Rightarrow \lambda \geq 14 - p \in \mathbf{Z}$ 이면 근사식이 아닌 Shift에 의한 연산이 등식 조건으로 성립한다. 그러나, 식 (7) 에서 

$$
\mathcal{X} = 10 \cdot 2^{\lambda - 10 + k \cdot m} =
\begin{cases}
\in \mathbf{Z}    & m = 0 \\
\notin \mathbf{Z} & m \in \mathbf{Z}[1, 5]
\end{cases}
$$

즉, $q$ 가 6의 배수인 경우에만 Shift 연산과 Gaussian 함수에 의한 양자화와 동일하게 된다. 

그 외의 경우에는,, Shift 연산에 의한 양자화에 오차가 있음을 의미하며, 오차의 크기에 따라,  예상하지 못한 결과가 나타날 수 있음을 의미한다. 


## Inverse Quantization

Inverse Qunatization은 기본적으로 다음과 같이 간단히 Quantization Step $q^s \in \mathbf{R}$을 곱하는 것으로 완료된다..

$$
Q^{-1}(q, X^Q) = X^Q \cdot q^s 
\tag{9}
$$

하지만,  Quantization Step 은 실수이므로 부호화 및 복호화에서는 이를 정수로 바꾸어야 하며 이를 위한  정수화 Scale 변수로 $2^6$ 을 사용한다. 이를 앞에서 유도한 Quantization Step 식 (2)를 사용하여 식 (9)를 다시 나타내면 

$$
\begin{aligned}
Q^{-1}(q, X^Q) &= X^Q \cdot 0.625 \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor + k \cdot (q \mod 6)} \cdot 2^6 \\

&= X^Q \cdot \frac{5}{8} \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor + k \cdot (q \mod 6)} \cdot 2^3 \cdot 2^3 \\

&= X^Q \cdot 40 \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor + k \cdot (q \mod 6)} 
\end{aligned}

\tag{10}
$$

$m = q \mod 6$ 이고, 위에서 구한 각 $m$에 대한 $k$을 통해 $40 \cdot 2^{km}$ 을 HEVC 에서는 **Level Scale** 이라 한다. HEVC 표준에 구현된 값과 다음의 Python Code를 통해 구한 값을 비교하면 다음 표와 같다.

~~~python
>>> npA = np.array([ 0.625,  0.703,  0.797,  0.891,  1.   ,  1.125])
>>> npQA = npA[1:6]
>>> npK = np.log2(npQA/0.625) * 1/np.array(list(range(1, 6)))
>>> npm = list(range(1, 6))
>>> LS = 40 * np.power(2, npk * npm)
~~~

|m      | 0   | 1   | 2   | 3   | 4   | 5   |
|---    |---  |---  |---  |---  |---  |---  |
| Eval  |40.0 |44.99|51.01|57.02|64.0 |71.99|
| HEVC  |40   |45   |51   |57   |64   |72   |

HEVC 표준에서는 식 (10)에 추가적으로 양자화 변환계수의 Scale 값을 추가하게 되는데 이 스케일 값은 $2^4$ 이다. 또한, 입력데이터의 비트심도와 변환 부호화의 크기에 따른 부호화 스케일 값을 위해 위의 값은 $2^{shift}$ 값으로 나누어 져야 하며, 여기에 Shift 값으로 나누어지기 때문에 반올림에 의한 정수값을 만들기 위한 항을 추가해야 한다. 이를 추가하게 되면 식 (10)은 다음과 같이 다시 쓸 수 있다.

$$
\begin{aligned}
Q^{-1}(q, X^Q) 

&= \left [X^Q \cdot 40 \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor + k \cdot m + 4} \right] \gg shift \\

&= \left \lfloor X^Q \cdot 40 \cdot 2^{\left \lfloor \frac{q}{6} \right \rfloor + k \cdot m + 4} + 2^{shift -1}\right \rfloor \gg shift 

\end{aligned}

\tag{11}
$$
