Annealing Effect를 포함하는 Quantized Quasi Newton 
====

Quasi Newton 방법을 사용하면,  (다른 모든 방법론과 마찬가지로..) Local에서 빠져나오지 못하는 문제점이 있다.  고전적인 문제이기는 하지만, 이를 회피하기 위한 방법론으로서는 역시, Annealing Algorithm을 적용해야 한다. 

## Conjugate Gradient에서의 Armijo Rule
Conjugate Gradient의 경우 다음 두 가지 방법 중 하나를 선택한다.

- **Polak - Riebel Formula**

$$
r_i = - \frac{\langle g_{i+1}, g_{i+1} \rangle - \langle g_i, g_{i+1} \rangle}{\| g_i \|^2}
$$

- **Fletcher-Reeves Formula **
   - Since for the quadratic case, $\langle g_{i+1}, g_{i} \rangle = 0$, that results can be extended.
$$
r_i = - \frac{\| g_{i+1} \|^2}{\| g_i \|^2}
$$

이 중,  **Fletcher-Reeves Formula ** 방법은 적절하게 Armijo 방법론에서 $\alpha$를 줄이게 되면 상당히 정확하게 Local Minima를 탈출하여 Global 을 찾아간다.

그러나, Line Search에 의한 경우에는  올바른 최적점을 찾아가지 못한다. 이 부분은 향후 투가 연구 및 Debug가 필요할 것으로 보인다.



## Step-size evaluated by Armijo's rule

Armijo Rule에 따른 Step size 계산시 사용된다.  Gradient Descent 이므로 (-) 기호가 되어야 해서 Lecture 에서는 $f(x_i + \beta^k h_i)$ 로 되어 있는 것을 (물론 그 위에 $h_i = -\nabla f(x_i)$ 로 정의 되어 있다.) $f(x_i - \beta^k h_i)$로 수정한다.

$$
\lambda_i = \lambda(x_i) \triangleq \arg \max_{k \in \mathbb{N}}  \{ \beta^k | f(x_i - \beta^k h_i) - f(x_i) \leq -\beta^k \cdot \alpha \| \nabla f(x_i) \|^2 \}
$$

 - 위에서 정의된 Armijo Rule 을 개량할 필요성이 있다. 가장 큰 부분은 $\alpha$ 에대한 부분인데, 이 항이 고정된 값으로 되어 있다. 만일, 이 값을 조금씩 작게 만들 수 있다면 보다 적응적으로 움직이는 알고리즘이 될 것이다.

 - 예를 들어 현재 코드에서는 만일 Armijo Rule이 빠르게 $\lambda = \beta^k$ 를 찾지 못한다면, Chk_freq를 보고 $\alpha$ 값을 적절히줄이는 방식으로 구성하였다. 즉, $\alpha<0$ 이므로 $\alpha_{\text{next}}  = \alpha^k$ 이 되도록 구성하였다.
    - 하지만 그렇게 효과가 있지는 않다. 보다 적절한 방법이 필요할 것으로 생각된다.




## Local Minima 문제점

Quasi Newton의 경우 게산되어 나오는 $h$ 값은 매우 크다. 


