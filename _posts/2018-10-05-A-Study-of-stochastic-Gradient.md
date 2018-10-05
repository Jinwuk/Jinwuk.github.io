---
layout: post
title:  "A Study of Stochastic Gradient (English/Korean)"
date:   2018-10-05 23:45:00 +0900
categories: [Mathematics, Stochastic Calculus]
tags:
  - Stochastic Calculus
  - Stochastic Gradient
comments: true
---

본 문서는 구글에서 발표된 기계학습을 위한 Stochastic Gradient에 대한 연구[1]에 본인의 아이디어를 추가하여 구글 팀에서 제시된 Stochastic Gradient Rule을 보다 쉽게 구할 수 있는 방법론에 대한 연구이다. 
아울러, 본 알고리즘을 사용하여 변경된 기존 기계학습을 위한 목적함수와의 비교를 통해 실제, Stochastic Gradient가 적용될 경우 Wiener Process에 의해 어떠한 변화가 발생할 수 있는지를 고찰한다. 

This article illustrates a simple methodology to obtain the stochastic gradient rule provided by  Google's A.I. team based on their original research[1], by my idea based on stochastic calculus. 

In addition, compared to the objective function for a conventional machine learning algorithm by the represented stochastic scheme, I also provide some expectational results by the Wiener process employed in the stochastic gradient. 

## Gradient Identity

### Lemma 1

$$
\nabla_{\mu_i} \mathcal{N}(\xi | \mu, C) = - \nabla_{\xi_i} \mathcal{N}(\xi | \mu, C)
$$

#### proof of Lemma

$$
\begin{align}
\nabla_{\mu} \mathcal{N}(\xi | \mu, C) &= \frac{\partial}{\partial \mu} \frac{1}{\sqrt{2 \pi C}} \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) \\
&= \frac{1}{\sqrt{2 \pi C}} \frac{\partial}{\partial \mu}  \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) \\
&= \frac{1}{\sqrt{2 \pi C}} \frac{(\xi - \mu)}{C} \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) \\
\end{align}
$$

$$
\begin{align}
\nabla_{\xi} \mathcal{N}(\xi | \mu, C) &= \frac{\partial}{\partial \xi} \frac{1}{\sqrt{2 \pi C}} \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) \\
&= \frac{1}{\sqrt{2 \pi C}} \frac{\partial}{\partial \xi} \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) \\
&= \frac{1}{\sqrt{2 \pi C}} -\frac{(\xi - \mu)}{C} \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) 
\end{align}
$$

Thus,

$$
\nabla_{\mu_i} \mathcal{N}(\xi | \mu, C) = - \nabla_{\xi_i} \mathcal{N}(\xi | \mu, C)
$$

**Q.E.D.**

### Bonnet's Theorem
Let $f(\xi) : \mathbb{R}^d \rightarrow \mathbb{R}$ be a integrable and twice differentiable function. The gradient of the expectation of $f(\xi)$ under a Gaussian distribution $\mathcal{N}(\xi | \mu, C)$ with respect to the mean $\mu$ can be expressed as the expectation of the gradient of $f(\xi)$.

$$
\nabla_{\mu_i} \mathbb{E}_{\mathcal{N}(\mu, C)} [f(\xi)] = \mathbb{E}_{\mathcal{N}(\mu, C)}[\nabla_{\xi_i} f(\xi)]
$$

#### proof

$$
\begin{align}
\nabla_{\mu_i} \mathbb{E}_{\mathcal{N}(\mu, C)} [f(\xi)] &= \int \nabla_{\mu_i} \mathcal{N}(\xi | \mu, C) f(\xi) d\xi \\
&= - \int \nabla_{\xi_i} \mathcal{N}(\xi | \mu, C) f(\xi) d\xi  \;\;\;\;\;\;\text{by Lemma 1 } \\
&= [\int \mathcal{N}(\xi | \mu, C) f(\xi) d\xi]_{\xi = -\infty}^{\xi = \infty} + \int \mathcal{N}(\xi | \mu, C) \nabla_{\xi_i} f(\xi) d\xi \\
&= \int \mathcal{N}(\xi | \mu, C) \nabla_{\xi_i} f(\xi) d\xi \\
&= \mathbb{E}_{ \mathcal{N}(\mu, C)} [\nabla_{\xi_i} f(\xi)]
\end{align}
$$

### Lemma 2

$$
\nabla_{C} \mathcal{N}(\xi | \mu, C) = \frac{1}{2} \frac{\partial^2 }{\partial \xi^2} \mathcal{N}(\xi | \mu, C)
$$

#### proof of Lemma

$$
\begin{align}
\nabla_{C} \mathcal{N}(\xi | \mu, C) &= \frac{\partial }{\partial C} \frac{1}{\sqrt{2 \pi C}} \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) \\
&= \frac{1}{\sqrt{2 \pi C}} \cdot -\frac{1}{2} \cdot C^{-1} \cdot \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) + \frac{1}{\sqrt{2 \pi C}} \cdot (\xi - \mu)^2 \cdot \frac{1}{2} \cdot C^{-2} \cdot \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) 
\end{align}
$$

From Lemma 1

$$
\begin{align}
\frac{\partial^2 }{\partial \xi^2} \mathcal{N}(\xi | \mu, C) &= \frac{\partial }{\partial \xi} \frac{\partial }{\partial \xi} \mathcal{N}(\xi | \mu, C) \\
&= \frac{\partial }{\partial \xi} \frac{1}{\sqrt{2 \pi C}} -\frac{(\xi - \mu)}{C} \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) \\
&= \frac{1}{\sqrt{2 \pi C}} \cdot -C^{-1} \cdot \exp \left(- \frac{(\xi -\mu)^2}{2C} \right) + \frac{1}{\sqrt{2 \pi C}} \cdot (\xi - \mu)^2 \cdot C^{-2} \exp \left(- \frac{(\xi -\mu)^2}{2C} \right)
\end{align}
$$

Thus,

$$
\nabla_{C} \mathcal{N}(\xi | \mu, C) = \frac{1}{2} \frac{\partial^2 }{\partial \xi^2} \mathcal{N}(\xi | \mu, C)
$$

**Q.E.D.**

### Price's Theorem
Under the same condition as the theorem of Bonnet, the gradient of the expectation of $f(\xi)$ under a Gaussian distribution $\mathcal{N}(\xi| 0, C)$ with respect to the covariance $C$ can be expressed in terms of the expectaion of the Hessian of $f(\xi)$ as

$$
\nabla_{C_{i, j}} \mathbb{E}_{\mathcal{N}(0,C)} [f(\xi)] = \frac{1}{2} \mathbb{E}_{\mathcal{N}(0,C)} [\nabla_{\xi_i, \xi_j} f(\xi)]
$$

#### proof

$$
\begin{align}
\nabla_{C_{i, j}} \mathbb{E}_{\mathcal{N}(0,C)} [f(\xi)] &= \int \nabla_{C_{i, j}} \mathcal{N}(\xi | 0,C) f(\xi) d\xi \\
&= \frac{1}{2} \int \nabla_{\xi_i, \xi_j} \mathcal{N}(\xi | 0,C) f(\xi) d\xi \;\;\;\;\;\;\text{From Lemma 2} \\
&= \frac{1}{2} \int \mathcal{N}(\xi | 0,C) \nabla_{\xi_i, \xi_j} f(\xi) d\xi \;\;\;\;\;\;\text{부분 적분 2번 적용} \\
&= \frac{1}{2} \mathbb{E}_{\mathcal{N}(0,C)} [\nabla_{\xi_i, \xi_j} f(\xi)]
\end{align}
$$

### Theorem 3

$$
\nabla_{\theta} \mathbb{E}_{\mathcal{N}(\mu,C)} [f(\theta)] = \mathbb{E}_{\mathcal{N}(\mu,C)} \left[ (\nabla_{\theta} f(\theta) )^T \frac{\partial \mu}{\partial \theta} + \frac{1}{2} Tr \left( H \frac{\partial C}{\partial \theta} \right) \right]
$$

#### proof

$$
\begin{align}
\nabla_{\theta} \mathbb{E}_{\mathcal{N}(\mu,C)} [f(\theta)] &= \frac{\partial}{\partial \theta} \mathbb{E}_{\mathcal{N}(\mu,C)} [f(\theta)] \\
&= \frac{\partial }{\partial \mu} \frac{\partial \mu}{\partial \theta} \mathbb{E}_{\mathcal{N}(\mu,C)} [f(\theta)] + \frac{\partial }{\partial C} \frac{\partial C}{\partial \theta} \mathbb{E}_{\mathcal{N}(\mu,C)} [f(\theta)] \\
&= \frac{\partial }{\partial \mu} \mathbb{E}_{\mathcal{N}(\mu,C)} [f(\theta)] \cdot \frac{\partial \mu}{\partial \theta} + \frac{\partial }{\partial C}  \mathbb{E}_{\mathcal{N}(\mu,C)} [f(\theta)] \cdot \frac{\partial C}{\partial \theta} \\
&= \mathbb{E}_{\mathcal{N}(\mu,C)} [\nabla_{\theta} f(\theta)] \cdot \frac{\partial \mu}{\partial \theta} + \frac{1}{2} \mathbb{E}_{\mathcal{N}(\mu,C)} Tr(\mathbb{E}_{\mathcal{N}(\mu,C)}[H(f(\theta))]\cdot \frac{\partial C}{\partial \theta} \\
&= \mathbb{E}_{\mathcal{N}(\mu,C)} \left[ (\nabla_{\theta} f(\theta))^T \frac{\partial \mu}{\partial \theta} + \frac{1}{2} Tr(H(f(\theta) \cdot \frac{\partial C}{\partial \theta} ) \right]
\end{align}
$$


## Analysis of Stochastic Differential Equation
### SDE Analysis
I think that the above mentioned stochastic gradient rule by the  following equation to induce the former term and following term by Ito differential. ,   
$$
\nabla_{\theta} [f(\theta)] = \nabla_{\theta} \mathbb{E}_{\mathcal{N}(\mu,C)} [f(\theta)] + \nabla_{w_t} f(\theta)
$$

In other words, If 

$$
z_t = \mu(z_t) + \sigma(z_t) w_t  
$$

then,

$$
dz_t = \frac{\partial \mu}{\partial z_t} dt + \frac{\partial \sigma}{\partial z_t} dw_t
$$

thus,  by Ito Calculus, let $\theta_t = z_t$ and I analyze the equation such that

$$
\begin{align}
df(\theta_t) &= (\nabla_{\theta_t} f(\theta_t))^T d\theta_t + \frac{1}{2} Tr \left( H(f(\theta_t)) d\theta_t^2 \right)\\
&= (\nabla_{\theta_t} f(\theta_t) )^T \left(\frac{\partial \mu}{\partial \theta_t} dt + \frac{\partial \sigma}{\partial \theta_t} dw_t \right) + \frac{1}{2} Tr \left (H(f(\theta_t)) \left(\frac{\partial \sigma}{\partial \theta_t} \right) \left( \frac{\partial \sigma}{\partial \theta_t} \right)^T \right) dt \\
&= \left[ (\nabla_{\theta_t} f(\theta_t) )^T \frac{\partial \mu}{\partial \theta_t} +  \frac{1}{2} Tr \left( H(f(\theta_t)) \frac{\partial C}{\partial \theta} \right) \right] dt + (\nabla_{\theta_t} f(\theta_t) )^T \frac{\partial \sigma}{\partial \theta_t} dw_t
\end{align}
$$

정의에 의해 $\mathbb{E}_{\mathcal{N}(\mu,C)}$ 에 대한 $df(\theta_t)$의 평균을 구하면, Ito SDE의 Martingale Property에 의해

$$
\mathbb{E}_{\mathcal{N}(\mu,C)}[df(\theta_t)] = \mathbb{E}_{\mathcal{N}(\mu,C)} \left[ (\nabla_{\theta_t} f(\theta_t) )^T \frac{\partial \mu}{\partial \theta_t} +  \frac{1}{2} Tr \left( H(f(\theta_t)) \frac{\partial C}{\partial \theta} \right) \right] dt
$$

그러므로

$$
\mathbb{E}_{\mathcal{N}(\mu,C)} \left[ \frac{df(\theta_t)}{dt} \right] = \mathbb{E}_{\mathcal{N}(\mu,C)} \left[ (\nabla_{\theta_t} f(\theta_t) )^T \frac{\partial \mu}{\partial \theta_t} +  \frac{1}{2} Tr \left( H(f(\theta_t)) \frac{\partial C}{\partial \theta} \right) \right] 
$$

The above result is the equal to the result of Theorem 3, same to the following

$$
\begin{align}
\mathbb{E}_{\mathcal{N}(\mu,C)} \left[ \frac{df(\theta_t)}{dt} \right] &= \nabla_{\theta} \mathbb{E}_{\mathcal{N}(\mu,C)} [f(\theta)] \\
\mathbb{E}_{\mathcal{N}(\mu,C)} \left[ df(\theta_t) \right] &= \nabla_{\theta} \mathbb{E}_{\mathcal{N}(\mu,C)} [f(\theta)] dt
\end{align}
$$

따라서, 평균값에 대한 Directional Derivation 의 결과가 정의와 일치하므로 확률미분방정식에 의한 해석이 기존의 해석[1]과 동일함을 알 수 있으며 중간 단계의 보조정리 없이 한번에 동일한 결과를 얻을 수 있음을 알 수 있다. 뿐만 아니라 SDE를 사용하여 이의 Fokker-Plank Equation을 얻을 수 있으므로 Stochastic Gradient 뿐만 아니라, Monte Carlo 기반의 알고리즘 역시 적용할 수 있다.

Consequently, since the result of Directional Derivation with respect to the average is equal to the definition, the analysis based on the  stochastic differential equation is same to the conventional anaysis[1] without any lemmas. 
In addition, since the Fokker-Plank equation of the stochastic gradient by the proposed methodology using SDE, it is possible to develop the algorithm based on the Monte-Carlo method.  


### Using suitable co-ordinate transformations

어떤 Spherical Gaissisn $ \epsilon \approx \mathcal{N}(0, \mathbf{I})$ 로부터 Gaussian 분포 $\mathcal{N}(\mu, \mathbf{C})$를 얻는 다고 가정하자. 그리고 변환 방정식은 $y = \mu + \mathbf{R}
\epsilon$ 이며 $\mathbf{C} = \mathbf{R}\mathbf{R}^T$ 라고 가정하자.  이때, $\mathbf{R}$에 대한 기대값의 Gradient는 다음과 같다.

$$
\nabla_{\mathbf{R}} \mathbb{E}_{\mathcal{N}(\mu, \mathbf{C})} [f(\xi)] = \nabla_{\mathbf{R}} \mathbb{E}_{\mathcal{N}(0, \mathbf{I})}[f(\mu + \mathbf{R}\epsilon)] = \mathbb{E}_{\mathcal{N}(0, \mathbf{I})}[\epsilon (\nabla_{\xi} f(\xi))^T]
$$

## Example : Deep Latent Gaussina Model 알고리즘에서의 Gradient 변화

Let the matrix $\mathbf{V} \in \mathbb{R}^{N \times D}$ to refer to the full data set of the observations $\mathbf{v}_n = [v_{n1}, \cdots, v_{nD}]^T$.
임의의 Latent 벡터의 영향을 살펴보기 위한 Maginal likelihoiod는 다음과 같다.

$$
\begin{align}
\mathcal{L} &= - \log p(\mathbf{V}) = - \log \int p(\mathbf{V}|\xi, \theta^g) p(\xi, \theta^g) d\xi \\
&= - \log \int \frac{q(\xi)}{q(\xi)} p(\mathbf{V}|\xi, \theta^g) p(\xi, \theta^g) d\xi \\
&\leq \mathcal{F}(\mathbf{V})= D_{KL} [q(\xi)||p(\xi)] - \mathbb{E}_q [\log p(\mathbf{V}|\xi, \theta^g) p(\xi, \theta^g)]
\end{align} \tag{1}
$$

where $\theta^g$ is the parameter of generative model.
- The approximate posterior 

$$
q(\xi | \mathbf{V}, \theta^r) = \prod_{n=1}^N \prod_{l=1}^L \mathcal{N}(\xi_{n,l}|\mu_l(\mathbf{v}_n), \mathbf{C}_l(\mathbf{v}_n))
$$

where the mean $\mu_l(\cdot)$ and covariance $\mathbf{C}_l(\cdot)$ are generic maps represented by deep neural networks.
Parameters of the $q$-distribution are denoted by the vector $\theta^r$.
이때, DLGM의 free Energy는 방정식 (1)에서 KL-Divergence를 통해 다음과 같이 구해질 수 있다.

$$
\begin{align}
D_{KL}[\mathcal{N}(\mu, \mathbf{C}) || \mathcal{N}(0, \mathbf{C}) ] &= \frac{1}{2} \left[ tr\mathbf{C} - \log |\mathbf{C}| + \mu^T \mu - D\right] \\
\mathcal{F}(\mathbf{V}) &= -\sum_n \mathbb{E}_q \left[ \log_p(\mathbf{v}_n | h(\xi_n) \right] + \frac{1}{2 \kappa} \| \theta^g \|^2 + \frac{1}{2} \sum_{n,l} \left[ \| \mu_{n,l} \|^2 + tr(\mathbf{C}_{n,l}) - \log |\mathbf{C}_{n,l}| - 1 \right]
\end{align}
\tag{2}
$$

자세한 증명은 다음 사이트를 참조한다.
The detailed proof is represented in the following URL :
http://jnwhome.iptime.org/?p=354

$\theta^r$에 대한 직접 Gradient의 경우는 매우 난해하기 떄문에 가우시안 분포의 변환 행렬 $\mathbf{R}$을 사용한다. such that $\mathbf{C} = \mathbf{R}\mathbf{R}^T$
그러면 co-ordunate Transform 에 대한 Gradient 를 사용한다. (이때 $f(\xi) = \log_p (\mathbf{v} | h(\xi)) $ )

$\mathcal{F}(\mathbf{v})$ 의 평균 $\mu_l(\mathbf{v})$와 Factor $\mathbf{R}$에 대한 Gradient는 다음과 같다.

$$
\begin{align}
\nabla_{\mu_i} \mathcal{F}(\mathbf{v}) &= -\mathbb{E}_q \left[ \nabla_{\xi_l} \log p (\mathbf{v} | \mathbf{h}(\xi)) \right] + \mu_l \\
\nabla_{R_{l, i,j}} \mathcal{F}(\mathbf{v}) &= -\frac{1}{2} \mathbb{E}_q \left[ \epsilon_{l, j} \nabla_{\xi_{l, i}} \log p (\mathbf{v} | \mathbf{h}(\xi)) \right] + \frac{1}{2} \nabla_{R_{l, i,j}} \left[ tr \mathbf{C}_{n,l} - \log |\mathbf{C}_{n.l} | \right]
\end{align}
$$

이에따라 $\nabla_{\theta_j^r}\mathcal{F}(\mathbf{v})$는 다음과 같다.

$$
\nabla_{\theta^r} \mathcal{F}(\mathbf{v}) = \nabla_{\mu} \mathcal{F}(\mathbf{v})^T \frac{\partial \mu}{\partial \theta^r} + tr\left( \nabla_{\mathbf{R}} \mathcal{F}(\mathbf{v}) \frac{\partial \mathbf{R}}{\partial \theta^r}  \right)
$$

따라서 Backpropagation Algorithm에서 사용되는 Descent Step은 다음과 같이 정의된다.

$$
\Delta \theta^{g,r} = -\Gamma^{g,r} \nabla_{\theta^{g,r}} \mathcal{F}(\mathbf{V})
$$

여기서 $\Gamma^{g,r} $는 Diagonal pre-conditioning matrix 이다.

## AdaGrad (for adaptive gradient algorithm) 

Adagrad는 2011년 최초로 발표된 Adaptive Stochastic Gradient Descent 방법으로서 Learning rate를 Gradient에 적응적으로 가변 시키는 방식의 알고리즘이다.
$g_{\tau} = \nabla Q_i(w)$ 인 Gradient 일떄, 다음과 같은 Matrix  $G$를 놓는다.

$$
G = \sum_{\tau = 1}^t g_{\tau} g_{\tau}^T
$$

$G$의 Diagoinal 성분은 그러므로 다음과 같다.

$$
G_{j,j} = \sum_{\tau = 1}^t g_{\tau}^2
$$

이때, Update 방정식을 다음과 같이 놓는다.

$$
w(t+1) \triangleq w(t) - \eta \; \text{diag}(G)^{\frac{1}{2}} \circ g 
$$

이때, $\circ$ 는 elementwise operation으로서 element별로 살펴보면 다음과 같다.

$$
w_j(t+1) \triangleq w_j(t) - \frac{\eta}{\sqrt{G_{j,j}}} g_j
$$

이 방법은 Convex Problem에 잘 맞는 알고리즘이나 non-convex 문제에서도 우수한 성능을 보인다.

그러나 해당 방법은 General Conjugate Method에서 Fletcher-Reeves Formula 방법론과 유사해 보인다.
Conjugate 방법론에서는 

$$
\begin{align}
x_{i+1} &= x_i - \lambda_i h_i \\ 
g_{i+1} &= Hx_{i+1} + d  \\
h_{i+1} &= g_{i+1} + h_i r_i 
\end{align}
$$

이때, $r_i$는  

$$
r_i = -\frac{\langle Hh_i, g_{i+1} \rangle }{\langle h_i , Hh_i \rangle}
$$

로 주어지고 특별히 Fletcher-Reeves 방법론에서는 다음과 같다.

$$
r_i = - \frac{\| g_{i+1} \|^2}{\| g_i \|^2}
$$

위 방법론에서 $g$는 똑같이 $\nabla Q$로 정의되므로 Conjugate 방법론을 정리해보면 

$$
\begin{align}
x_{i+1} &= x_i - \lambda_i h_i = x_i - \lambda_i (g_i + r_{i-1} h_{i-1} ) = x_i - \lambda_i (g_i - \frac{\| g_{i} \|^2}{\| g_{i-1} \|^2} h_{i-1} ) \\
&= x_i - \frac{\lambda_i}{\| g_{i-1} \|^2} (\| g_{i-1} \|^2 g_i - \| g_{i} \|^2 h_{i-1} )
\end{align}
$$

이때, 

$$
\lambda_i = \frac{\eta}{\| g_i \|} 
$$

로 놓고 h-Conjugate를 적용하면 간단히 Adagrad 알고리즘이 된다.  하지만 이러한 접근은 너무나 편의적인 접근으로 보이기 떄문에 아래에 나와 있는 SDE on manifold를 통하여 관련 알고리즘을 보다 엄밀하게 볼 필요도 있다. 왜냐하면 다양체에서의 Metric Tensor를 만일, Gradient와 관련된 어떤 것으로 정의할 수 있으면 Gradient를 Geodesic 을 정의하는 속도 벡터로 놓고 살펴볼 수 있기 때문이다.


## Stochastic Differential Equation (SDE) on Manifold

먼저, Manifold가 아닌 경우에 대하여는 다음과 같다.

### SDE and Fokker Plank Equation
다음 SDE에 대하여

$$
dx_t = h(x_t) dt + H(x_t) dW_t, \;\;\; x_t, h(\cdot) \in \mathbb{R}^n, \; dW_t \in \mathbb{R}^m \; H(\cdot) \in \mathbb{R^{n \times m}}
$$

State $x_t$ 에 대하여 출력 $y_t = f(x_t) \in \mathbb{R} $ 라고 하면 이에 대한 SDE는 다음과 같다.

$$
dy_t = \left(\sum_j \frac{\partial f_i}{\partial x_j}h_j(x_t)+ \frac{1}{2} \sum_{k,l} \frac{\partial f_i^2}{\partial x_k \partial x_l} [H(x_t)H^T(x_t)]_{kl}\right)dt + \sum_{k,l} \frac{\partial f_i}{\partial x_j} H_{kl}(x_t)dW_{tl}
$$

만일, $x = x_t$ 이고 $y = x_{t -dt}$ 이고 state에 대한 SDE를 따른다고 하고 Transition Probability $p(x|y,dt)$를 생각하면

$$
\begin{align}
\int_{\mathbb{R}^n} (x - y) p(x|y,dt) dy &= \mathbb{E}(x - y) = h(x_t)dt \\
\int_{\mathbb{R}^n} (x - y)(x - y)^T p(x|y,dt) dy &= \mathbb{E}(x - y)(x - y)^T = \sum_k^m H_{ik}(x_t)H_{kj}^T(x_t)dt \\
\end{align}
$$
이에 대하여 Fokker-Plank 방정식은 다음과 같다.

$$
\frac{\partial p(x|y,t)}{\partial t} = - \sum_{i=1}^n \frac{\partial}{\partial x_i}(h_i(x_t)p(x|y,t)) + \frac{1}{2} \sum_{i,j=1}^n \frac{\partial^2}{\partial x_i \partial x_j} \left( \sum_{k=1}^m H_{ik}(x_t) H_{kj}^T(x_t) p(x|y,t)\right)
$$

- 즉, 순수 SDE 해석은 Stochastic Gradient Rule을 Expectation 만을 Update 한다고 가정할때 사용할 수 있으며
- Fokker-Plank Equation 해석은 $p(x|y,t)$를 사용하여 Monte Carlo 방식으로 Weight를 Update할 때 사용할 수 있다.

### SDE and Fokker Plank Equation on Manifold
만일 Manifold $M$의 Metric tensor가 $G = [g_{ij}]$ 로 주어질 경우 (Inverse는 $G^{-1} = [g^{ij}]$ )

$$
\frac{\partial p(x|y,t)}{\partial t} = - |G|^{-\frac{1}{2}}\sum_{i=1}^n \frac{\partial}{\partial x_i}(|G|^{\frac{1}{2}}h_i(x_t)p(x|y,t)) + \frac{1}{2} |G|^{-\frac{1}{2}}\sum_{i,j=1}^n \frac{\partial^2}{\partial x_i \partial x_j} |G|^{\frac{1}{2}}\left( \sum_{k=1}^m H_{ik}(x_t) H_{kj}^T(x_t) p(x|y,t)\right)
$$

그러나 일반적인 SDE의 경우 Manifold 위에서의 일반적인 Martingale항을 정의하는 것은 대단히 어렵다. 그 이유는 $dW_t$ 가 일반적인  Manifold 위에 어떻게 정의 되는가 자체가 어렵기 때문이다. 일단, Manifold 위의 Tangent Space상의 Wiener Process중, Orthogonal Component는 없다고 가정하고, Horizontal 성분만 있다고 가정해도 Wiener Process에 대한 정의를 내리기 위해서 Geodesic위에서 먼저 Horizontal Vector Field를 정의하여야 Local coordinates 자체를 정의할 수 있다. 즉, 

만일 Parameterized curve $t \rightarrow u_t e_m = e_m^k (t) X_k$ 로 주어졌다고 가정하면 (여기서 $X_k = \frac{\partial }{\partial x^k}$, $X_{km} = \frac{\partial }{\partial e_m^k}$ )
Parallel Transportaion 조건 ($e_m$ 은 $\mathbb{R}^d$ 상의 Coordinate Index)

$$
\dot{e}_m^k(t) + \Gamma_{jl}^k(x_t)\dot{x}_t^j e_m^l = 0
$$

에서 

$$
\dot{e}_m^k(t) = -e_i^j e_m^l \Gamma_{jl}^k(x_t), \;\;\;\dot{x}_0^j = e_i^j
$$

일 경우 다음과 같은 Brownian Motition 이 주어질떄 ($\circ$ 는 Starnotovici SDE 기호)

$$
\begin{align}
dX_t^i &= e_j^i(t) \circ dW_t^j \\
de_j^i(t) &= - \Gamma_{kl}^i(X_t) e_j^l(t) e_k^m(t) \circ dW_t^m
\end{align}
$$

Euclidean Brownian Motion $dM_t = \sigma(X_t)dB_t$ 로 주어졌을 때, Manifold위의 Horizontal Brownian Motion $X_t$ 는 다음과 같이 유도된다.

$$
dX_t^i = \sigma_j^i(X_t) dB_t^i - \frac{1}{2} g^{lk}(X_t) \Gamma_{kl}^i(X_t)dt, \;\;\; g^{ij} = \sum_{k=1}^d e_k^i e_k^j
$$

이를 사용하여 Operator를 만들던가 혹은 Girsanov Theorem등을 사용하여 Wiener Process와 Martingale을 분리하여 SDE를 성리시켜야 한다.

Local Coordinater에서 Generator는 다음과 같다. 

$$
\Delta_M f = \frac{1}{\sqrt{G}} \frac{\partial}{\partial x^j} \left(\sqrt{G} g^{ij} \frac{\partial f}{\partial x^i} \right) = g^{ij} \frac{\partial}{\partial x^i} \frac{\partial f}{\partial x^j} + b^i \frac{\partial f}{\partial x^i}
$$

where

$$
b^i = \frac{1}{\sqrt{G}} \frac{\partial (\sqrt{G} g^{ij})}{\partial x^j} \;\; \Rightarrow b^i = g^{jk} \Gamma_{jk}^i
$$

#### Note
즉,

$$
b^i = \frac{1}{\sqrt{G}} \frac{\partial (\sqrt{G} g^{ij})}{\partial x^j} = \frac{\partial g^{ij}}{\partial x^j} = \frac{\partial }{\partial x^j} \sum_{k=1}^d e_k^i e_k^j = \nabla_{X_j} \sum_{k=1}^d e_k^i e_k^j 
$$

그러므로 Let $X_k = e_k^i$ or $X_k = e_k^j$ 이면

$$
\nabla_{X_j} \sum_{k=1}^d e_k^i X_k \cdot e_k^j = \sum_{k=1}^d e_k^i e_k^j \nabla_{X_j} X_k = g^{ij} \Gamma_{jk}^i
$$



[1] Danilo J. Rezende, Shakir Mohamed, Daan Wierstra, "Stochastic Backpropagation and Approximate Inference in Deep Generative Models", Proc. ICML, 2014. : arXiv:1401.4082v3.
