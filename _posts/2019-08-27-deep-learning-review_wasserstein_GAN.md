---
layout: post
topic: deep-learning
title: 주관적인 논문리뷰 - Wasserstein GAN - Facebook AI Research
---
[실제 논문은 여기로](https://arxiv.org/pdf/1701.07875.pdf)  

<br>

#### 1. 대략적인 논문 설명  

GAN을 발전시킨 논문이다.  
GAN의 문제점 중 하나는 학습이 어렵다는 것이었는데, 해당 논문은 GAN에서 학습이 어려운 이유가  
실제 분포와 생성 분포의 차이를 JSD로 추정하였기 때문이라고 주장한다.  
이에 두 분포의 차이를 추정하는 다른 방법인 Wasserstein 을 적용하여 optimize를 시도한 내용을 담은 논문이다.  


이 때, 저자가 두 분포의 차이를 정의할 때 신경쓴 점은 sparsity이다.  
즉 R^n 위에 위치한 분포가 사실 더 낮은 차원인 R^m (m < n) 위에서 표현 가능할 때,  
저자는 실제 분포와 생성 분포의 차이를 연속적으로 나타낼 수 있도록 정의했는가를 중요하게 생각했다.  


예를 들어, 강아지 사진은 3(rgb)x64(w)x64(h) 라고 하더라도,  
실제 강아지를 표현하는 분포의 파라미터 개수가 3x64x64는 아닐 것이다. 이보다 더 작을 것이다.  
그러나 최종적인 분포는 3x64x64 위에서 표현되므로 분포가 sparse하다고 볼 수 있다.  
Wasserstein GAN은 이러한 문제점을 해결하고자 하는 내용을 담고 있다.  


<br>

#### 2. EM distance 또는 Wasserstein-1  

위에서 말한 문제점을 해결하고자 논문에서 제시한 방법이 EM distance, 또는 Wasserstein-1 이다.  
EM distance은 어떤 곳에 뭉쳐있는 진흙더미를 다른 곳으로 옮길 때 드는 최소 비용을 계산하는 것으로부터 파생되었다고 한다.  

$$
Let \; P_r, \; P_g \; be \; distributions. \\
Then \; we \; can \; think \; about \; set \; of \; all \; joint \; distributions \; of \; P_r \; and \; P_g, \; denoted \; by \; \prod(P_r, P_g) \\
Then, \; W(P_r, P_g) := \underset{\gamma \in \prod(P_r, P_g)}{inf} E_{(x,y) \sim \gamma}(||x-y||)
$$


<br>

#### 3. wasserstein-1이 좋은 추정인가  

wasserstein-1이 원하는 성질을 갖고 있음을 아래의 과정을 통해 증명한다.  

1. generator 가 locally lipschitz 이고, local lipschitz constant가 존재하여 E(z~p)[L(&theta;, z)] &le; &infin; 을 가정한다.  
2. generator가 파라미터에 대하여 연속이면, 실제 분포와 생성 분포의 Wasserstein-1 이 generator 파라미터에 대하여 연속임을 증명한다.  
3. 가정 0 아래에서 실제 분포와 생성 분포의 Wasserstein-1 이 lipschitz임을 증명하여 연속임을 보이고, Rademacher's theorem 으로부터 differentiable almost everywhere 임을 보인다.  
4. E(z~p)[&#124;z&#124;] < &infin; 이면 generator에 대하여 가정 1이 성립됨을 증명한다.  
5. 따라서 생성 분포와 실제 분포의 wasserstein-1 이 연속이고, differentiable almost everywhere 임을 보인다.  
이로써 wasserstein-1이 원하는 성질을 갖고 있음을 주장한다.  


<br>

#### 4. wasserstein-1을 어떻게 추정할 것인가  

wasserstein-1 이 좋은 성질을 갖고 있음을 보였지만, 여전히 어떻게 wasserstein-1을 추정할 것인가 하는 문제가 남아있다.  

위에서 보다시피 Wasserstein-1 을 구하기 위해서는  
1) 두 분포의 모든 결합 분포를 알아야 하며,  
2) 그 중 infimum 을 찾아야 한다.  

이는 현실적으로 매우 어려운 가정이다.  
따라서 논문에서는 Kantorovich-Rubinstein duality를 이용하여 infimum을 구하는 과정을 대체한다.  

[Kantorovich-Rubinstein duality 보기](https://www.sciencedirect.com/science/article/pii/S0723086911000430)

<br>

#### 5. weight clip  

Kantorovich-Rubinstein duality를 사용하기 위해서는 discrimnator가 최소 k-lipschitz 여야 한다.  
그러나 학습 과정에서 k-lipschitz를 smooth하게 강제할 방법을 찾지 못하여 discriminator 학습 후 weight를 clip 한다.  

<br>

#### 6. 논문을 읽고  

분포의 차이를 어떻게 추정할까 하는 것은 어려운 일이다. 정답이 존재하지도 않는다.  
특히나 sparse한 분포라면 더욱 난감할 것이다.  
이러한 상황 속에서 원하는 성질을 찾아내고, 이를 충족하는 함수를 찾아내는 것이 흥미로웠다.  
또한 wasserstein에는 현실적인 제약이 많았는데, 이를 헤쳐나가는 모양도 재미있었다.  


한편, k-lipschitz를 충족하기 위해 weight를 clip하는 것이 어떻게 보면 무식한 방법일 수 있는데,  
해당 논문 이후 발전된 WGAN-GP 모델에서는 이러한 문제를 해결하는 방법을 제시한다.  

결국 부족함을 인정하고, 개선해나가는 과정에서 발전이 이루어지는 것 같다.
