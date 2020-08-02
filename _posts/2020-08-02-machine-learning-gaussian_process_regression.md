---
layout: post
topic: machine-learning
title: Gaussian Process Regression
---

<br>

### 1. 소개

Gaussian Process Regression 은 데이터가 Gaussian Process 로부터 생성되었다는 가정 하에 데이터에 fitting 하는 방법이다.  
따라서 Gaussian Process 를 알아야 하고, 이를 위해서 Multivariate Gaussian Distribution 에 대해 알아야 한다.  

---

### 2. Multivariate Gaussian Distribution

Univariate Gaussian Distribution 은 평균과 분산의 두 개 파라메터로 정의된다.  
반면 Multivariate Gaussian Distribution 은 n 차원 벡터라고 가정하면  
각 차원의 평균과 각 차원 간의 Covariance 가 필요하므로 n + n*n 개의 항이 필요하다.  

이 때 부분 벡터로 구성된 conditional distribution 도 정규분포이고 아래는 그 증명이다.  

$$
\begin{bmatrix} x \\ y \end{bmatrix} \sim N(\begin{bmatrix} u_x \\ u_y \end{bmatrix}, \Sigma)
\; where \; x \in R^{r \times 1}, \; y \in R^{m \times 1} \; and 
\; \Sigma = \begin{bmatrix} \Sigma_{xx} \; \Sigma_{xy} \\ \Sigma_{yx} \; \Sigma_{yy} \end{bmatrix} \\
Then, \; E(x|y) = u_x + (\Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1})(y - u_y) \;
and \; \Sigma_{x|y} = \Sigma_{xx} - \Sigma_{xy} \Sigma_{yy}^{-1} \Sigma_{yx} \\
or, \; x_{|y} \sim N(E(x|y), \Sigma_{x|y}) \\
Proof) \\
Let \; x' = x - u_x \; and \; y' = y - u_y \\
p(x|y) = \frac{p(x,y)}{p(y)} = \frac
{\frac{exp(-\frac{1}{2}\begin{bmatrix} x' \\ y' \end{bmatrix}^T \Sigma^{-1} \begin{bmatrix} x' \\ y' \end{bmatrix})}{(2\pi)^{n/2}|\Sigma|^{1/2}}}
{\frac{exp(-\frac{1}{2} y'^T \Sigma_{yy}^{-1} y')}{(2\pi)^{m/2}|\Sigma_{yy}|^{1/2}}} \\
Firstly \; we \; calculate \; |\Sigma| / |\Sigma_{yy}| \; and \; \begin{bmatrix} x' \\ y' \end{bmatrix}^T \Sigma^{-1} \begin{bmatrix} x' \\ y' \end{bmatrix} - y'^T \Sigma_{yy}^{-1} y' \\
\begin{bmatrix} I \quad -\Sigma_{xy}\Sigma_{yy}^{-1} \\ O \quad\quad\quad\quad I \end{bmatrix} 
\begin{bmatrix} \Sigma_{xx} \; \Sigma_{xy} \\ \Sigma_{yx} \; \Sigma_{yy} \end{bmatrix}
\begin{bmatrix} I \quad\quad\quad\quad O \\ -\Sigma_{yy}^{-1}\Sigma_{yx} \quad I \end{bmatrix}
= \begin{bmatrix} \Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx} \quad O \\ O  \quad\quad\quad\quad\quad\quad\quad \Sigma_{yy} \end{bmatrix} \\
Thus \; det(\Sigma) = det(\Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx}) det(\Sigma_{yy}) \; 
because \; the \; determinant \; of \; triangular \; matrix \; is \; a \; product \; of \; diagonal \; terms. \\
Let \; S := \Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx} \\
Then \; |\Sigma| / |\Sigma_{yy}| = |S| = |\Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx}| \\
Now \; we \; we \; calculate \; \begin{bmatrix} x' \\ y' \end{bmatrix}^T \Sigma^{-1} \begin{bmatrix} x' \\ y' \end{bmatrix} - y'^T \Sigma_{yy}^{-1} y' \\
\Sigma^{-1} = \left(\begin{bmatrix} I \quad -\Sigma_{xy}\Sigma_{yy}^{-1} \\ O \quad\quad\quad\quad I \end{bmatrix}^{-1} 
              \begin{bmatrix} \Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx} \quad O \\ O  \quad\quad\quad\quad\quad\quad\quad \Sigma_{yy} \end{bmatrix}
              \begin{bmatrix} I \quad\quad\quad\quad O \\ -\Sigma_{yy}^{-1}\Sigma_{yx} \quad I \end{bmatrix}^{-1}\right)^{-1}
= \begin{bmatrix} I \quad\quad\quad\quad O \\ -\Sigma_{yy}^{-1}\Sigma_{yx} \quad I \end{bmatrix} 
  \begin{bmatrix} \Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx} \quad O \\ O  \quad\quad\quad\quad\quad\quad\quad \Sigma_{yy} \end{bmatrix}^{-1}
  \begin{bmatrix} I \quad -\Sigma_{xy}\Sigma_{yy}^{-1} \\ O \quad\quad\quad\quad I \end{bmatrix} 
= \begin{bmatrix} I \quad\quad\quad\quad O \\ -\Sigma_{yy}^{-1}\Sigma_{yx} \quad I \end{bmatrix} 
  \begin{bmatrix} S^{-1} \quad O \\ O \quad \Sigma_{yy}^{-1} \end{bmatrix}
  \begin{bmatrix} I \quad -\Sigma_{xy}\Sigma_{yy}^{-1} \\ O \quad\quad\quad\quad I \end{bmatrix} \\
Then, \;
\begin{bmatrix} x' \\ y' \end{bmatrix}^T \Sigma^{-1} \begin{bmatrix} x' \\ y' \end{bmatrix} = 
\begin{bmatrix} x' \\ y' \end{bmatrix}^T
\begin{bmatrix} I \quad\quad\quad\quad O \\ -\Sigma_{yy}^{-1}\Sigma_{yx} \quad I \end{bmatrix} 
\begin{bmatrix} S^{-1} \quad O \\ O \quad \Sigma_{yy}^{-1} \end{bmatrix}
\begin{bmatrix} I \quad -\Sigma_{xy}\Sigma_{yy}^{-1} \\ O \quad\quad\quad\quad I \end{bmatrix}
\begin{bmatrix} x' \\ y' \end{bmatrix}
= 
\begin{bmatrix} x' - \Sigma_{xy}\Sigma_{yy}^{-1}y' \\ y' \end{bmatrix}^T
\begin{bmatrix} S^{-1} \quad O \\ O \quad \Sigma_{yy}^{-1} \end{bmatrix}
\begin{bmatrix} x' - \Sigma_{xy}\Sigma_{yy}^{-1}y' \\ y' \end{bmatrix} 
= (x' - \Sigma_{xy}\Sigma_{yy}^{-1}y')^T S^{-1} (x' - \Sigma_{xy}\Sigma_{yy}^{-1}y') + y'^T \Sigma_{yy}^{-1} y'
\\
Thus, \begin{bmatrix} x' \\ y' \end{bmatrix}^T \Sigma^{-1} \begin{bmatrix} x' \\ y' \end{bmatrix} - y'^T \Sigma_{yy}^{-1} y'
= (x' - \Sigma_{xy}\Sigma_{yy}^{-1}y')^T S^{-1} (x' - \Sigma_{xy}\Sigma_{yy}^{-1}y') + y'^T \Sigma_{yy}^{-1} y' - y'^T \Sigma_{yy}^{-1} y'
= (x' - \Sigma_{xy}\Sigma_{yy}^{-1}y')^T S^{-1} (x' - \Sigma_{xy}\Sigma_{yy}^{-1}y') 
= (x - u_x - \Sigma_{xy}\Sigma_{yy}^{-1}(y - u_y))^T S^{-1} (x - u_x - \Sigma_{xy}\Sigma_{yy}^{-1}(y - u_y)) \\
Finally, p(x|y) = \frac
{\frac{exp(-\frac{1}{2}\begin{bmatrix} x' \\ y' \end{bmatrix}^T \Sigma^{-1} \begin{bmatrix} x' \\ y' \end{bmatrix})}{(2\pi)^{n/2}|\Sigma|^{1/2}}}
{\frac{exp(-\frac{1}{2} y'^T \Sigma_{yy}^{-1} y')}{(2\pi)^{m/2}|\Sigma_{yy}|^{1/2}}}
= \frac
{exp(-\frac{1}{2} (x - u_x - \Sigma_{xy}\Sigma_{yy}^{-1}(y - u_y))^T S^{-1} (x - u_x - \Sigma_{xy}\Sigma_{yy}^{-1}(y - u_y)))}
{(2\pi)^{(n-m)/2}|S|^{1/2}} \\
Indeed, \; x_{|y} \; also \; follows \; gaussian \; distribution \; with \; 
mean \; of \; u_x + \Sigma_{xy}\Sigma_{yy}^{-1}(y - u_y) \; 
and \; covariance \; matrix \; \Sigma_{xx} - \Sigma_{xy}\Sigma_{yy}^{-1}\Sigma_{yx}
$$

---

### 3. Gaussian Process 란

Gaussian Process 는 Random Process 가 Gaussian Distribution 을 따르는 것을 의미한다.  
$$
Let \; f: X -> F \; is \; a \; random \; process. \\
Then \; for \; any \; S \subset X \; if \; f(S) \; is \; a \; gaussian \; distribution \;
we \; call \; f \; is \; a \; gaussian \; process
$$

---

### 4. Gaussian Process Regression 란

데이터 D = (X, y) 가 평균이 0 인 Gaussian Process 에서 sampling 되었다고 가정하여 적합하는 것이다.  
이 때 커널 함수를 정의해야 하는데, 실질적인 커널 함수의 역할은 X 에서의 거리 차이에 따른 y 에서의 covariance 를 어떻게 정의할 것인지와 관련이 있다.  
이 때 보통 커널 함수의 하이퍼 파라메터를 training data 에 fitting 하는 식으로 학습이 진행된다.

---

### 5. Kernel 함수

가장 대표적인 커널 함수로 RBF 커널이 있다. (
$$
RBF(x, y) = se^{-\gamma ||x-y||^2} \quad s, \; \gamma > 0
$$
)

그 외에도 다양한 함수가 존재한다. ([Wikipedia 참고](https://en.wikipedia.org/wiki/Gaussian_process#Usual_covariance_functions))  

---

### 6. Gaussian Process Regression 학습

위의 RBF 커널 함수의 경우 두 개의 파라메터 s, r 이 존재한다.  
따라서 training data 에 대하여 위 두 파라메터를 최적화할 필요가 있다.  
최적화 방법에도 여러가지가 있겠으나 가장 간단하게 MLE 를 사용할 수 있다.  
$$
\log p(y|X) = -\frac{1}{2}y^T\Sigma_{s, \gamma}^{-1}y - \frac{1}{2}\log |\Sigma_{s, \gamma}| + constant
$$

---

### 7. Gaussian Process Regression 추론

학습을 통해 적절하게 covariance 를 구성하였다. 이후 새로운 샘플 x 에 대한 추론을 한다고 가정해보자.  
데이터가 Gaussian Process 를 가정에 의하여 기존 training data 에 x 를 추가해도 gaussian distribution 이 된다.  
또한 커널 함수를 결정하고 파라메터를 최적화 하였으므로 각각의 covariance 를 구할 수 있다.  
또한 conditional distribution 또한 특정한 평균과 분산을 따르는 gaussian distribution 임을 알고 있다.  
따라서 x 에 대하여 우리는 특정한 평균과 분산을 갖는 정규분포를 추정할 수 있다.  
이것이 Gaussian Process Regression 과정이다.

---

### 8. Advantage & Disadvantage

큰 장점 중 하나는 Non Linear Regression 을 수학적으로 아름답게 이끌어 낼 수 있다는 것일 것이다.  
또한 분포를 추정함으로써 uncertainty 를 추정할 수 있다는 장점이 있다.  


반면 단점은 역시 scalable 이 어렵다는 것일 것이다. 새로운 training data 가 추가되었을 때에  
분포를 업데이트 하기 위해서 처음부터 새로이 fitting 해야 하는 번거로움이 있다. (물론 이러한 단점을 개선한 다양한 모델이 존재한다.)  


또 다른 단점 중 하나는 커널 함수에 의존적이라는 것이다. 잘 되기 위하여서 데이터 형태에 적합한 커널을 선택해야 한다.  
하지만 그것이 어렵다는 것이 문제일 듯 한다.