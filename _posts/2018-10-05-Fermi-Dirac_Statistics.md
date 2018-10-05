---
layout: post
title:  "Fermi-Dirac Statistics (written with Korean) "
date:   2018-10-05 20:45:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
  - Fermi-Dirac Statistics
comments: true
---

통계역학에서 입자의 존재를 나타내는 통계는 입자의 성질에 의해 다음과 같이 구별된다.

|종류  | 의미   |
|---|----|
|Maxwell-Boltzmann 통계|고전 통계, 입자는 상호 구별 가능하며 에너지 준위에 몇개라도 들어갈 수 있다.|
|Fermi-Dirac 통계 | Fermion을 위한 통계, 입자는 상호 구별 불가능이며 에너지 준위에 하나만 들어갈 수 있다.|
|Bose-Einstein 통계 | Boson을 위한 통계, 입자는 상호 구별 불가능이며 에너지 준위에 몇개라도 들어갈 수 있다.|

![Fig01](https://github.com/Jinwuk/md/blob/master/img/General_Science/Particle_Statistics.png?raw=true)
(2개의 입자가 3개의 에너지 준위에 들어가는 경우 각 통계적 경우의 수)

## Fermi-Dirac 분포함수의 유도 

Fermi-Dirac 통계를 유도하기 위해 $i$ 번째 준위군에 $g_i$ 개의 준위 수가 있다고 가정하고 이떄 입자수가 $N_i$ 개 있다고 가정하자.
그림에서 처럼 Fermi-Dirac 통계를 유도하기 위해 $g_i$개의 통에 $N_i$개의 공을 넣는 경우의 수와 같은 문제이다.
맨 처음에 첫번쨰 공을 넣는 경우를 생각하며 $g_i$개의 통 중 $N_i$개의 공 중 하나가 $j$번째 통에 들어갈 확률은 다음과 같다.

$$
P_{j_1} = \frac{N_i}{g_i}
$$

그러면 나머지 통 중 하나에 들어갈 확룰은

$$
P_{j_2} = \frac{N_i-1}{g_i - 1}
$$

이 순서를 계속하면 공이 점유할 수 있는 전 확률은 각각 독립사건 이므로 

$$
\begin{align*}
P &= P_{j_1} P_{j_2} \cdots \\
  &= \frac{N_i}{g_i} \frac{N_i - 1}{g_i - 1} \cdots \frac{1}{g_i - N_i + 1} \\
  &= \frac{N_i !}{g_i (g_i -1) \cdots (g_i - N_i + 1)} \\
  &= \frac{N_i ! (g_i - N_i)!}{g_i !}
\end{align*}
$$

통에 공을 넣을 수 있는 방법의 횟수는 위 확률의 역수 이므로

$$
\begin{align*}
W &= W_1 W_2 \cdots W_n \\
  &= \frac{g_1 !}{N_1 ! (g_1 - N_1)!} \cdot \frac{g_2 !}{N_2 ! (g_2 - N_2)!} \cdots \frac{g_n !}{N_n ! (g_n - N_n)!} \\
  &= \prod_i \frac{g_i !}{N_i ! (g_i - N_i)!}
\end{align*}
$$

따라서 1,2,3 인 준위에 $N_1, N_2, N_3 \cdots$ 인 입자를 분배시키는 전체 분배 방법의 수는 

$$
W=\prod_i \frac{g_i !}{N_i ! (g_i - N_i)!}
$$

그런데, $N_i, g_i, g_i-N_i >> 1$ 이므로 스털링의 근사식을 사용하면

$$
ln W = \sum_i \left\{ g_i ln g_i - N_i ln N_i - (g_i -N_i) ln (g_i - N_i) \right\}
$$

한편, 입자 전체가 갖는 에너지 및 입자의 총수는 일정하므로 

$$
\sum_i E_i N_i = U, \;\; \sum_i N_i = N
$$

인 관계가 있다. 각 식을 $N_i$ 에 대하여 미분하면 

$$
\partial ln W = -\sum_i \left\{ ln N_i - ln (g_i - N_i) \right\} \partial N_i = 0 \\
\sum_i E_i \partial N_i  = 0 \\
\sum_i \partial N_i = 0
$$

Largrangian 을 사용하면 두개의 등식 제한 조건이 걸리는 것이므로 (E_i < 0 일 수는 없기 때문에...)
Largrangian 계수 $\alpha, \beta$를 사용하면

$$
\partial ln W - \alpha \partial N - \beta \partial E = 0
$$

이를 각각 대입하여 해석하면

$$
\sum_i \left\{ ln \frac{g_i - N_i}{N_i} -\alpha - \beta E_i\right\} \partial N_i = 0 \\
ln \frac{g_i - N_i}{N_i} = \alpha + \beta E_i \\
\frac{g_i - N_i}{N_i} = e^{\alpha + \beta E_i} \\
\frac{g_i }{N_i} = 1 + e^{\alpha + \beta E_i}
$$

Since $P_i = \frac{N_i}{g_i}$,

$$
P_i = \frac{N_i }{g_i} = \frac{1}{1 + e^{\alpha + \beta E_i}}
$$

여기에서 열 역학적 고려를 추가하면

$$
\beta = \frac{1}{\kappa T}, \;\; \alpha = - \frac{\mu}{\kappa T}
$$

이고 $\mu$는 Chemistry Potential 이며 $\mu$ 대신 $E_F$라는 기호를 사용한다. 이를 고려하면, 

$$
f(E) = \frac{1}{e^{\frac{E-E_F}{\kappa T}}+ 1}
$$

이것이 페르미-디랙 분포함수이다.

## Maxwell-Bolzmann 분포 (혹은 Gibb's 분포)와의 관계

위의 Fermi-Dirac 분포에서 $E - E_F \gg 1$의 경우에는 분모의 1은 아무런 의미가 없다. 그러므로

$$
\begin{align*}
f(E) &\approx e^{(E - E_F)/\kappa T} \\
     &\approx A e^{-\frac{E}{\kappa T}}
\end{align*}
$$

이는 다음의 Gibb's 분포와 같은 것이다.

$$
f(E_i) = \frac{1}{Z} e^{-\frac{E_i}{\kappa T}}
$$

where $Z = \sum_i e^{-\frac{E_i}{\kappa T}}$.