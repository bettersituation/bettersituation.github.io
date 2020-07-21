---
layout: post
topic: machine-learning
title: PCA (Principal Component Analysis)
---

<br>

### 1. 소개  

회사에서 사용하게 될 일이 있어 PCA 를 알아보게 되었다.  
예전에도 대략적인 느낌은 알고 있었지만 막상 그 과정을 다 이해하려고 하니 생각보다 많은 과정이 필요했다.  
PCA 를 이론적으로 알기 위해서는 SVD 를 알아야 하고, SVD 를 알기 위해서는 Spectral Theorem 을 알아야 한다.  
그리고 Spectral Theorem 을 알기 위해서는 그 전에 알아야할 것들이 있다.  
이렇듯 PCA 를 이해하는 데에 필요한 Theorem 마다 포스트를 작성한다.  


PCA 를 이해하는 데에 필요한 Theorem 은 SVD (Singular Value Decomposition) 이다.  
SVD 에 대한 내용 및 증명은 이 포스트를 보자

<br>

---

### 2. PCA 란

PCA 란 주어진 데이터를 그대로 보지 않고 중요도에 따른 축 변환을 수행하여 해석하는 것으로,  
일반적으로 가장 큰 중요도를 갖는 몇 개 벡터의 coordinate 값만 사용하는 식으로 사용한다.  


여기서 말하는 중요도라는 것은 무엇일까?  
중요도라는 것은 의미가 상당히 모호하지만 PCA 에서는 분산이라는 느낌으로 접근했고,  
분산이 가장 큰 축이 가장 중요한 축이라고 해석한다.  
분산을 사용한 이유는 아마도 엔트로피와 연관이 있을 것이다.  
주어진 분포에 따라 그 값은 다르겠으나 일반적으로 분산이 크면 클수록 엔트로피 값이 커지기 때문이다.  


따라서 결국 PCA 는 분산이 가장 큰 축을 찾는 것이다.  
이 때 각 축은 직교한다.

---

### 3. 주의점

PCA 를 사용할 때 첫 째로 주의해야 하는 점은 각 feature 의 평균을 0 으로 맞춰야 한다는 것이다.  
PCA 가 분산을 중심으로 해석하기 때문이다.  
모듈마다 자동으로 평균을 빼주는 과정이 포함될 수도 있다.  

또한 각 feature 별로 scaling 이 필요할 수 있다.  
예를 들어 사람의 키, 몸무게 데이터로부터 주성분을 분석하고자 할 때  
mm 단위로 측정된 키와 ton 단위로 측정된 몸무게를 두고 주성분을 분석하면 당연하게도 주성분 벡터는 키에 많은 영향을 받을 것이다.  
그렇기에 PCA 수행 전에 각 feature 별로 scaling 이 필요한지 아닌지, 필요하다면 얼마나 필요한지 확인해야 한다.  

---

### 4. PCA Theorem

PCA Theorem 은 아래와 같다. 막상 찾아보니 생각보다 별 것은 없었던 듯 하다.  
오히려 SVD, Spectral Theorem 이 더 흥미롭게 느껴졌다.

$$
Let X \in R^{n \times p} \; be \; an \; observation \; matrix \; s.t. x_i \in R^{1 \times p} \; is \; an \; observation \; 
s.t. \; X = 
\begin{bmatrix}
x_1 \\
\vdots \\
x_n \end{bmatrix} \\

Then \; we \; can \; find \; w_1 = \underset{|w|=1}{argmax} \; ||Xw||^2 \\
Then \; we \; can \; find \; w_2 = \underset{|w|=1}{argmax} \; ||Xw||^2 \; where \; w \perp \; w_1 \\
... \\
w_p = \underset{|w|=1}{argmax} \; ||Xw||^2 \; where \; w \perp \; w_i \; for \; all \; 1 \le i \le p-1
\\
Then \; we \; can \; define \; T \; by \; letting
\; W = 
\begin{bmatrix}
w_1 \; \cdots \; w_p 
\end{bmatrix} \; and \; T = XW \\
\\
T \; is \; a \; desired \; transformed \; matrix
$$

---

### 5. PCA with SVD

위에 기술한 것이 PCA 의 아이디어이다. 실제 계산할 때에는 계산 상 편리함을 위해 SVD 나 Covariance 를 이용하는데  
이는 사실 위 계산 과정이 SVD 를 계산할 때에 이미 적용되는 것이기 때문일 것이다.  
SVD 를 이용하면 다음과 같이 표현할 수 있다.  

$$
Let X \in R^{n \times p} \\
Then \; we \; can \; find \; orthonormal \; matrix \; U \in R^{n \times n} \; and \; V \in R^{p \times p}, \\
and \; \Sigma \in R^{n \times p} \; is \; descending \; ordered \; where \; \sigma_{ii} \ge 0 \; and \; \sigma_{ij} = 0 \quad if \quad i \ne j \\
s.t. X = U\Sigma V^* \\
$$
이 때 PCA 의 정의에 의하여 자연스럽게 V = W 가 성립하고 결국 다음 식이 성립한다.
$$
T = XW = U\Sigma V^*W = U\Sigma W^*W = U\Sigma
$$

---

### 6. PCA with Covariance

Covariance 를 이용하는 것도 위 과정과 유사하다. 데이터의 평균을 빼주고 필요하다면 각 피쳐 별로 Scaling 을 수행한다.  
그렇게 생성된 데이터 매트릭스가 X 라고 하자.  
$$C := cov X = \frac{X^*X}{n-1} \in R^{p \times p}$$ 라고 하자.  


Covariance Matrix 는 symmetric 하고 positive semi definite matrix 이므로 C 를 대각화하면 고유값은 음수가 아니며, 고유벡터는 직교한다. ($$V^{-1}CV = D$$)  
이 때 V = W 가 성립하고 T = XW 가 성립한다.


Energy Content g 는 아래와 같이 정의하고 주로 몇 개의 차원에 대하여 분석할 것인지에 대한 임계치로 사용된다.  
$$g_k = \sum_{i=1}^{k}{D_{ii}} \; and \; use \; like \; finding \; L \; s.t \; \frac{g_L}{g_p} \ge 0.9$$

---

### 7. 개선된 방법론

- PCA 는 feature 의 선형 결합으로 구성된다. 이러한 PCA 의 한계를 극복하는 방법론으로 엘라스틱맵(Elastic map), 추측치 분석(Principal geodesic analysis)와 커널 PCA 등이 있다.
- 다중 선형을 일반화하여 텐서로 확장된 다중 PCA (MPCA, Multilinear PCA) 방법론이 있다.  
- PCA 는 squared error 를 최소화하는 관점에서는 수힉적으로 최적의 방법이 맞지만 이상치에 민감하다. 가중 PCA 는 이상치에 강인하게 PCA 를 수행한다.  
- PCA 는 사실 상 모든 데이터의 선형 결합으로 표현된다. 따라서 특정한 몇 개 데이터의 선형 결함으로 PCA 를 수행하기 위해 희소 PCA(sPCA, Sparse PCA) 가 제안되었다.

---

### 8. 느낀 점

- PCA 를 막연하게 알고 있었는데, 생각보다 PCA 자체에는 별 내용이 없다고 느껴졌다.  
- 수학적으로는 Spectral Theorem, 알고리즘 적으로는 SVD 가 더 중요하다고 느껴졌다.
