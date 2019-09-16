#  Convergence analysis for Stochastic Gradient Descent


---
layout: post
title:  "Convergence analysis for Stochastic Gradient Descent"
date:   2019-11-11 01:45:00 +0900
categories: [Mathematics, Machine Learning]
tags:
  - Manifold Denosing
  - Machine Learning
comments: true

---

* Table of Contents
{:toc}


본 내용은 모두를 위한 컨벡스 최적화 https://wikidocs.net/book/1896  의  https://wikidocs.net/18090 를 정리한 것이다. 


f는 convex이고 differentiable하며 **dom** f = R^n일 때 다음 식을 만족한다고 하자.
$$
\lVert \nabla f(x) - \nabla f(y) \rVert_2 \le L \lVert x - y \rVert_2 \text{ for any } x, y \text { and } L \gt 0
$$

$\nabla f$는 Lipschitz constant $L$에 대해  Lipschitz continuous하다고 말할 수 있다.

참고 : [[(Wikipedia) Lipschitz continuity](https://en.wikipedia.org/wiki/Lipschitz_continuity)]

## Convergence Theorem

**Gradient descent**는 fixed step size $t \le 1/L$에 대해 다음 식을 만족한다.  

$$
f(x^{(k)}) - f^{*} \le  \frac{ \lVert x^{(0)} - x^{*} \rVert^2_2 }{2tk} 
$$

Gradient decent가 fixed step size일때 convergence rate $O(1/k)$가 된다. 또한, $f(x^{(k)}) - f^{*} \le \epsilon$라면 $O(1/\epsilon)$의 반복이 필요하다.

## Proof

$\nabla f$는 Lipschitz continuous하며 $f$는 Lipschitz constant $L$을 계수로 하는 2차 항으로 된 quadratic upper bound를 갖는다. (Upper bound의 증명은  [06-03-02](https://wikidocs.net/18454) 절을 참조)

$$
\begin{align} 
f(y) \le f(x) + \nabla f(x)^T (y-x) + \frac{L}{2} \lVert y - x \rVert^2_2,  \space \space \forall x, y \in \mathbf{R}^n
\end{align}
$$

Gradient descent를 현재 위치 $x$에서 다음 위치 $x^+ = x - t \nabla f(x)$로 진행한다고 해보자. 위의 식에서 $y = x^+$라고 하고 전개해보자.

$$
\begin{aligned} 
f(x^+) 
& \le f(x) +  \nabla f(x)^T (x^+ - x) + \frac{L}{2} \lVert x^+ - x \rVert^2_2 \\ 
& = f(x) +  \nabla f(x)^T (x - t \nabla f(x) - x) + \frac{L}{2} \lVert x - t \nabla f(x) - x \rVert^2_2 \\ 
& = f(x) - t \nabla f(x)^T (\nabla f(x)) + \frac{L}{2} \lVert t \nabla f(x) \rVert^2_2 \\ 
& =  f(x) - t \lVert \nabla f(x)) \rVert^2_2 + \frac{Lt^2}{2} \lVert \nabla f(x) \rVert^2_2 \\ 
& =  f(x) - t ( 1 - \frac{Lt}{2} )\lVert \nabla f(x) \rVert^2_2 \\ 
& \le f(x) -  \frac{t}{2} \lVert \nabla f(x) \rVert^2_2 
\end{aligned}
$$

마지막 라인은 $t \le 1/L$이기 때문에 $Lt/2 \lt 1/2$이 된다. 따라서 다음과 같이 정리될 수 있으며 $f(x^+) \lt f(x)$임을 알 수 있다.

$$
f(x^+) \le f(x) -  \frac{t}{2} \lVert \nabla f(x) \rVert^2_2
$$

### Claim 
즉, 2차 함수 보다 큰 1차 함수를 발견하여 그것으로 대치하는 것이다.
$$
\frac{L}{2} t^2 - t \le -\alpha t \Rightarrow \frac{L}{2} t^2 - (1 - \alpha) t  \le 0
$$
을 만족하는 $\alpha$를 $0 < t < 1/L$ 에서 찾는 것이다.  $t = 1/L$ 을 대입하여 $\alpha$를 구하면 된다.



$f$ convex이기 때문에 다음과 같이 1차 미분의 특성을 만족한다. (즉, $f$는 convex이기 때문에 $x$에서의 접선보다 항상 윗쪽에 존재한다.)
$$
f(y)  \ge f(x) + \nabla f(x)^T (y-x), \space \space \forall x,y \in \text{dom} (f)  
$$

이 식에서 $y = x^{*}$라고 하면 다음과 같이 정리된다.

$$
f(x)  \le f(x^{*}) + \nabla f(x)^T (x-x^{*})
$$

이 convexity를 $f(x^+)$ 식과 합쳐서 전개해보자.

$$
\begin{aligned} 
f(x^+) 
& \le f(x) -  \frac{t}{2} \lVert \nabla f(x) \rVert^2_2 \\ 
& \le f(x^{*}) + \nabla f(x)^T (x-x^{*}) - \frac{t}{2} \lVert \nabla f(x) \rVert^2_2 \\ 
& = f(x^{*}) + \frac{1}{2t} ( \lVert x - x^{*} \rVert^2_2 -  \lVert x - x^{*} \rVert^2_2 - t^2 \lVert \nabla f(x) \rVert^2_2 + 2t \nabla  f(x)^T (x - x^{*}) )  \\ 
& = f(x^{*}) + \frac{1}{2t} ( \lVert x - x^{*} \rVert^2_2 -  (x -  x^{*})^T (x - x^{*}) - t^2 \nabla f(x)^T  \nabla f(x) + 2t \nabla f(x)^T (x - x^{*}) )  \\ 
& = f(x^{*}) + \frac{1}{2t} ( \lVert x - x^{*} \rVert^2_2 -  [(x -  x^{*})^T (x - x^{*}) + t^2 \nabla f(x)^T  \nabla f(x) - 2t \nabla f(x)^T (x - x^{*})] )  \\ 
&= f(x^{*}) + \frac{1}{2t} ( \lVert x - x^{*} \rVert^2_2 -  [(x - t  \nabla f(x)^T - x^{*})^T (x - t \nabla f(x)^T - x^{*})] )  \\ 
& = f(x^{*}) + \frac{1}{2t} ( \lVert x - x^{*} \rVert^2_2 -  \lVert  x - t \nabla f(x)^T - x^{*} \rVert^2_2 )  \\ 
& = f(x^{*}) + \frac{1}{2t} ( \lVert x - x^{*} \rVert^2_2 -  \lVert  x^+ - x^{*} \rVert^2_2 )  
\end{aligned}
$$

마지막 단계는 $x^+ = x - t \nabla f(x)$이기 때문이다. 단계 ii에 이 결과를 적용해 보면 다음과 같아진다.

$$
f(x^{(i)}) - f(x^{*}) \le \frac{1}{2t} ( \lVert x^{(i-1)}  - x^{*} \rVert^2_2 -  \lVert  x^{(i)} - x^{*} \rVert^2_2 )
$$
따라서, 위의 식을 $i = 1$에서 $k$까지 더하면 다음과 같이 된다.

$$
\begin{aligned} 
\sum_{i=1}^k f(x^{(i)}) - f(x^{*}) & \le \sum_{i=1}^k \frac{1}{2t} ( \lVert x^{(i-1)}  - x^{*} \rVert^2_2 -  \lVert  x^{(i)} - x^{*}  \rVert^2_2 )  \\ 

& = \frac{1}{2t} ( \lVert x^{(0)}  - x^{*} \rVert^2_2 -  \lVert   x^{(k)} - x^{*} \rVert^2_2 )  \\ & \le \frac{1}{2t} ( \lVert x^{(0)}  - x^{*} \rVert^2_2 )  
\end{aligned}
$$

마지막 단계에서 각 ii의 첫번째 항은 i−1i-1의 두번째 항으로 소거되어 최종적으로 첫번째 항과 마지막 항만 남게 된다. $f(x^{(k)})$가 non-increasing임을 적용하여 정리해 보면 다음과 같다.

$$
\begin{aligned} 
\frac{1}{k} \sum_{i=1}^k f(x^{(i)}) - f(x^{*}) \ge  \frac{1}{k} \sum_{i=1}^k f(x^{(k)}) - f(x^{*}) = f(x^{(k)}) - f(x^{*}) 
\end{aligned}
$$

이에 따라 최종 결과는 다음과 같다.

$$
f(x^{(k)}) - f(x^{*}) \le \frac{1}{2tk} ( \lVert x^{(0)}  - x^{*} \rVert^2_2 )
$$

이로써 Gradient descent의 Convergence Theorm이 증명되었다.