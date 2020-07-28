---
layout: post
topic: machine-learning
title: SVD (Singular Value Decomposition)
---

<br>

### 1. 소개  

PCA 를 하는 데에 기초가 되는 정리이다.  
SVD 는 또 다시 Spectral Theorem 에 기초하고 있는데, Spectral Theorem 을 보고 싶다면 이 포스트를 보자.  
SVD 는 PCA 보다 수학적 측면에서 중요한 듯 하다.  

---

### 2. SVD 란

SVD 란 임의의 m x n 행렬 M 이 주어졌을 때 orthonormal 행렬 U, V가 존재하고, diagonal 행렬 D 가 존재하여  
$$M = UDV^*$$ 으로 행렬 M 을 분해하는 것이다.  
행렬이 선형변환이라고 보았을 때 축변환 &rarr; 배수 &rarr; 축변환 이라는 매우 간단한 과정으로 선형변환을 분해했다고 볼 수도 있겠다.  

---

### 3. Singular Value, Vector 란

SVD 는 Singular Value Decomposition 의 약자이다. 여기서 Singular Value 라는 개념이 사용되었음을 알 수 있다.  
Singular Value 란 아래처럼 정의된다.  

$$
Let \; M \in R^{m \times n} \\
\exists \sigma \ge 0, \; \exists v \in R^{n \times 1}, \; \exists u \in R^{m \times 1} \\
if \; Mv = \sigma u \; and \; M^* u = \sigma v \; holds, \\
we \; call \; \sigma \; as \; singular \; value, \; v \; as \; right \; singular \; vector, \; u \; as \; left \; singular \; vector
$$

---

### 4. Singular value vs Eigenvalue

얼핏 보면 비슷한 듯 하지만 사실 되게 애매한 듯 하다.  
예를 들어 아래 행렬을 생각해보자.  

$$
\begin{pmatrix}
0 \; a \\
\frac{1}{a} \; 0
\end{pmatrix}
$$

이 행렬의 eigenvalue 는 -1, 1 인 반면, singular value 는 a, 1/a 이다.  
따라서 간단하게 생각하기는 힘들고 일반적으로 아래 성질이 증명되었다.  
\- singular value 의 최대값은 maximum eigenvalue 보다 작거나 같다.  
\- 행렬 M 이 normal 이라면 ($$M^*M = MM^* $$) singular value 는 eigenvalue 의 절대값이다.

---

### 5. SVD

SVD 증명은 아래와 같다.  

$$
Let \; M \in R^{m \times n} \\
Then \; M^*M \in R^{n \times n} and \; symmetric \; and \; positive \; semidefinite \\
Let \; \lambda_i \; be \; an \; eigenvalue \; of \; M^*M \; and \; v_i \; be \; a \; corresponding \; vector. \\
Then, \; \lambda_i \ge 0 \; because \; of \; positive \; semidefinite \; 
and \; \{v_i: \lambda_i > 0 \} \; is \; orthogonal \; because \; of \; symmetricity \\
Let \; \sigma_i = \sqrt{\lambda_i} \; and \; u_i = Mv_i / \sigma_i \; for \; \lambda_i > 0 \\
Then \; <u_i, u_j> = <Mv_i / \sigma_i, Mv_j / \sigma_j> = v_j^*M^*Mv_i / \sigma_i \sigma_j = \lambda_i v_j^*v_i / \sigma_i \sigma_j = \delta_{ij} \\
$$

$$
Let \; |\{\lambda: \lambda > 0\}| = r, \;
V = \begin{pmatrix}
v_1 \; ... \; v_r
\end{pmatrix} \in R^{n \times r}, \;
U = \begin{pmatrix}
u_1 \; ... \; u_r
\end{pmatrix} \in R^{m \times r} \; and \;
\Sigma = \begin{pmatrix}
\sigma_1 \; \cdots \; 0 \\
\vdots \; \ddots \; \vdots \\
0 \; \cdots \; \sigma_r
\end{pmatrix} \\
Then \; MV = U\Sigma
$$

$$
If \; we \; need \; we \; can \; exapnd \; \Sigma \; to \; be \; in \; R^{m \times n} \; by \; filling \; 0 \; and \\
V \; to \; be \; in \; R^{n \times n} \; by \; construct \; orthogonal \; basis \; 
from \; v_1, \; ..., \; v_r \; by \; using \; a \; process \; like \; gram-schmidt, \;
U \; to \; be \; in \; R^{m \times m} \; also. \\
Then \; MV = U\Sigma \to M = U\Sigma V^*
$$

---

### 6. SVD 의 의의

SVD 를 선형대수학의 꽃이라고 부르는 경우가 많다. 아마도 위에는 적어두지 않았지만 선형대수학의 중요한 정리 등을 총망라하여 SVD 를 하기 때문일 것이다.  
예를 들어 위에서는 딱히 쓸 일이 없어서 쓰지 않았지만 SVD 에는 Kernel Space 와 관련된 인사이트도 포함되어 있다.  
또한 임의의 선형변환, 심지어 다른 차원으로의 선형변환일지라도 basis 를 활용하여 매우 간단한 형태(각 축마다 몇 배로 늘려줄 것인가 하는) 로 변환된다는 것이 매력적이라고 할 수 있다.  
아마 내가 알지 못하는 더 깊은 내용도 당연히 있을 것이다만 이것으로도 일단은 충분하다고 본다.