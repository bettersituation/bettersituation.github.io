---
layout: post
topic: deep-learning
title: 주관적인 논문리뷰 - Generative Adversarial Nets - Ian J. Goodfellow
---
[실제 논문은 여기로](https://papers.nips.cc/paper/5423-generative-adversarial-nets.pdf)  

<br>
#### 1. 대략적인 논문 설명  

2014년에 발표되어 많은 주목을 받은 논문이다.  
classification이나 regresseion처럼 어떤 값을 예측하는 것이 아니라 데이터를 생성하는 모델이다.  
원본 데이터와 비슷한 데이터를 만드는 것을 목표로 한다.  

해당 모델은 크게 두 가지 과정으로 나뉜다.  
첫 째는 가짜 데이터를 만드는 과정이고, 둘 째는 원본 데이터와 가짜 데이터를 구분하는 과정이다.  

이 때 첫 째 과정을 담당하는 네트워크를 Generator, 둘 째 과정을 담당하는 네트워크를 Discriminator 라고 한다.  
Discriminator는 원본 데이터인지 아닌지 판단하는 역할을 하므로 최종 결과는 0~1 사이의 확률값으로 나타낸다.  

수치화된 목표를 다음과 같이 설정한다.  

$$
\underset{G}{min}\; \underset{D}{max} \; V(D,G) = \underset{G}{min}\; \underset{D}{max} \; E_{x \sim p_{data}(x)}[\log D(x)] + E_{z \sim p_z(z)} [\log(1 - D(G(z)))]
$$

해당 목표를 달성하기 위해 아래 과정을 반복한다.  
1) Update Discrimnator k-times  
2) Update Generator  
3) goto 1)  

<br>

#### 2. 수학적 근거  

**1. Global optimality**  

$$
Proposition) \; Assume \; G \; is \; fixed, \;
then \; optimal \; D_G^* (x)= \frac{p_{data}(x)}{p_{data}(x) + p_G(x)} \\
proof) \\
V(G,D) = \int_x p_{data}(x) \log D(x) + p_G(x) \log(1 - D(x)) dx \\
p_{data}(x) \log D(x) + p_G(x) \log(1 - D(x)) \; achieves \; its \; maximum \; value \; at \; D_G^* (x) \\
$$

$$
Theorem) \; Assume \; D = D_G^* , \; then \; global \; optimality \; is \; achieved \; if \; and \; only \; if \; p_{data} = p_G \\
V(G, D) = \int_x p_{data}(x) \log D(x) + p_G(x) \log(1 - D(x)) dx \\
= \int_x p_{data}(x) \log\frac{p_{data}(x)}{p_{data}(x) + p_G(x)} + p_G(x) \log\frac{p_G(x)}{p_{data}(x) + p_G(x)} dx \\
= \int_x p_{data}(x) \left(-\log2 + \log \frac{p_G(x)}{(p_{data}(x) + p_G(x))/2} \right) + p_G(x) \log\left(-\log2 + \frac{p_G(x)}{(p_{data}(x) + p_G(x))/2} \right) dx \\
= -\log4 + KL(p_{data}|\frac{p_{data}+p_G}{2}) + KL(p_G|\frac{p_{data}+p_G}{2}) \\
= -\log4 + 2 \cdot JSD(p_{data}|p_G) \\
but \; JSD \ge 0 \; and \; JSD(p_1|p_2) = 0 \; if \; and \; only \; if \; p_1 = p_2 \; holds. \\
Thus \; given \; statement \; holds.
$$

<br>

**2. Convergence of Generator**  

$$
Lemma) \; Assume \; D = D_G^* , \; then \; U(p_G) = V(G, D_G^* ) \; is \; convex \; in \; p_G \\
proof) \\
f(x): X \rightarrow R \; is \; convex \; \iff \forall \; 0 \le t \; \le 1, \; tx_1 + (1-t)x_2 \in X \; and \; f(tx_1 + (1-t)x_2) \le tf(x1) + (1-t)f(x_2) \\
Thus, \; we \; will \; show \; that \; f(q) = JSD(p|q) \; is \; convex \\
Firstly, \; q_* = tq_1 + (1-t)q_2 \in \left\{q\right\} absolutly \; because \; q_* \ge 0 \; and \int q_* = 1 \; definitely \; holds \\
Secondly, \; t \cdot KL(p|(p+q_1)/2) + (1-t)KL(p|(p+q_2)/2) \ge KL(p|(p+q_*)/2) \; holds \; by \; the \; fact \; that \\
t\log(p + q_1) + (1-t)\log(p + q_2) \le \log(p + q_*) \; holds \; because \; \log \; is \; concave \\
Thirdly, \; t \cdot KL(q_1|(p + q_1)/2) + (1-t) KL(q_2|(p + q_2)/2) \ge KL(q_*|(p + q_*)/2) \; holds \; by \; the \; fact \; that \\
if \; we \; let \; f(x) = x \log \frac{x}{p+x}, \; then \; \forall \; 0 \le x \le 1, \; f''(x) = \frac{p^2}{x(p+x)^2} \ge 0, \; which \; means \; f \; is \; convex
$$

$$
Theorem) \; Global \; convergence \; can \; be \; attained \; by \; a \; given \; process \\
proof) \\
U(p_G) \; is \; convex, \; so \; we \; can \; attain \; global \; optimality \; by \; using \; SGD
$$

<br>

#### 3. GAN의 의의  

GAN은 2014년 당시 기준 (내가 알기로) 새로운 생성 방법론을 제시했다.  
기존 생성 모델은 p_G 를 직접적으로 추정하여 데이터를 생성하는 반면,  
GAN은 p_G 를 직접적으로 추정하지 않고 데이터를 생성하기 때문이다.  

또한 서로 파라미터가 공유되지 않는 Discriminator와 Generator 두 개의 네트워크를 사용했다는 점에서도 재미있다.  
Discrimnator와 Generator 가 상대방 네트워크에 있어서 black box 라는 점을 생각해보았을 때,  
네트워크 모델의 강력함을 증명해낸 면도 있다.  

<br>

#### 4. GAN 이후  

GAN은 크게 두 가지 문제점을 안고 있다.  
첫 째로 증명할 때는 max log(1-D(G)) 로 해놓고, 실제 학습 시에는 min log(D(G)) 를 썼다.  
둘 째로 Generator와 Discriminator의 학습 정도가 엇비슷하지 않으면 Generator가 학습되지 않는 문제가 있다.  
셋 쨰로 원본 데이터의 분포와 생성 데이터의 분포의 거리를 JSD를 사용하여 추정했는데,  
JSD는 sparse manifold 에서 제대로 동작하지 않는다.  
이러한 문제점을 해결하기 위해서 발전된 모델이 나온다.  


<br>

#### 5. Ian J. Goodfellow의 두 편의 논문을 읽고  

GAN은 maxout에 이어 두번째로 읽은 Ian J. Goodfellow 의 논문이다.  
두 개의 논문을 읽으면서 느낀 점은 두 논문 모두 이상적인 상황에 대하여 증명한다는 것이다.  
아이디어와 실험 결과만 있는 논문도 존재하는데 이런 점에서 다른 논문과 차별화된다고 느꼈다.  
개인적으로 실험 결과만 있는 논문보다는 이렇게 이론적 바탕이 있는 논문이 더 흥미롭게 느껴진다.  
