---
layout: post
topic: machine-learning
title: Newey West Test
---

<br>

### 1. 소개  

회사 동료의 소개로 Newey West Test 를 알게 되었고, 궁금하여 더 찾아보았다.  
찾아보며 알게 된 것은 Newey West Test 는 기본 선형회귀에서 파생되었다는 것과,  
더 중요하게는 선형회귀에 대해 보다 자세히 알 수 있게 되었다.  

Wiki 문서를 참고하면 newey west Test 는 observation 이 
autocorrelation 과 heteroskedasticity 를 갖고 있을 때에 사용하기 적합하다고 한다.  

autocorrelation이 존재한다는 것은 각각의 observation 이 시계열로 주어졌을 때  
이전 값에 의하여 현재 값이 영향을 받는다는 것을 의미한다.  

heteroskedasticity 는 예측 값의 분산이 입력변수에 의존하여 변하는 것을 의미한다.  

그렇다면 일반적인 선형회귀 또는 T-test 와 Newey West Test 는 무엇이 다른가?  

결론을 말하면 입력변수에 대하여 추정된 계수는 같다.  
다만 그 계수의 유의성을 검증할 때 사용되는 standard deviation 이 다르다.

<br>

---

### 2. 선형회귀  

선형회귀는 아래처럼 간단한 식으로 표현할 수 있다.  

$$
Y = X \beta + \epsilon \\
where \\
Y \in R^{n \times 1} \; is \; a \; dependent \; variable \\
X \in R^{n \times k} \; is \; an \; independent \; variable \\
\beta \in R^{k \times 1} \; is \; a \; coefficient \; matrix \\
\epsilon \in R^{n \times 1} \; is \; an \; error \; term \\
$$

이 때 위 식을 최적화 하는, 즉 에러 텀을 최소화 하는 베타 불편추정값 및 분산은 아래와 같이 추정된다.
 ([\*참고자료](https://web.stanford.edu/~mrosenfe/soc_meth_proj3/matrix_OLS_NYU_notes.pdf))  

$$
\hat{\beta} = (X^* X)^{-1} X^* Y \\
Cov(\beta) = (X^* X)^{-1} X^* Cov(\epsilon) X (X^* X)^{-1}
$$

결국 기본적인 선형회귀와 다른 선형회귀의 차이점은 엡실론에 대해 어떻게 가정하느냐이다.  

기본 선형회귀 같은 경우는 등분산 및 독립 가정을 통해 엡실론의 Covariance 를 Identity matrix 의 배수로 가정한 것이다.  

반면 Newey West Test 같은 경우는 Covariance 에 heteroskedasticity 와 autocorrelation 를 반영할 수 있도록 가정한 것이다.  

<br>

---

### 3. Newey West Test

Newey West Test 는 아래와 같은 과정으로 진행된다.  
첫 째, 베타 추정량을 바탕으로 각 observation 에 대한 에러를 구한다.  

$$
u_i = Y - X_i \hat{\beta} \quad for \quad 1 \le i \le n
$$

<br>

둘 째, 엡실론의 Covariance 를 아래와 같이 추정한다.  

$$
Cov(\epsilon)_{ij} = w_{ij} u_i u_j \\
Where, \\
w_{ij} = w_{ji} \; and \\
w_{ij} = 1 \quad if \; i = j \\
$$

이 때 w(ij) 를 결정하는 방법은 kernel 로써 하이퍼파라메터이다.  
그러나 일반적으로 Lagging 길이를 정하여 아래와 같이 하는 하는 듯 하다.  

$$
L \; is \; an \; autocorrelation \; length \; hyperparameter. \\
Then, \\
if \; |i-j| \le L, \quad w_{ij} = 1 - \frac{|i-j|}{L+1} \\
else, \quad w_{ij} = 0
$$

<br>

셋 쨰로, 이렇게 추정된 엡실론의 Covariance 를 바탕으로 베타의 Covariance 를 계산한다.  
이로부터 나온 Variance 를 사용하여 베타 값에 대하여 T-test 를 진행하는 것이 Newey West Test 이다.

<br>

---

### 4. Newey West Test 의 주의점  

대부분의 모형이 그렇듯 하이퍼파라메터와 가정에 주의해야 한다.  
엡실론이 최근 엡실론에 크게 영향받는 것이 맞는지, Seasonal 한 특성은 없는지, 
역으로 받는 영향은 없는지 등에 주의해야 할 것이다.  

<br>

---

### 5. 느낀 점  

시간 거리에 따라 영향 정도가 감소하고 무조건 양의 영향을 미친다는 점에서 RBF kernel 이 떠올랐다.  
