---
layout: post
topic: deep-learning
title: 주관적인 논문리뷰 - Discriminator Actor Critic - Addressing sample efficiency and reward bias in adversarial imitation learning - Google Brain
---
[실제 논문은 여기로](https://openreview.net/pdf?id=Hk4fpoA5Km)  
[구현 코드는 여기로](https://github.com/google-research/google-research/tree/master/dac)

<br>
#### 1. 대략적인 논문 설명  

이 논문은 Imitation Learning의 계보를 그대로 있는 논문이다.  
그래서 Imitation learning 을 중점에 두고 봤을 때 특별한 부분을 찾기 어려웠다.  
논문 제목에서 나타나듯이 Imitation learning에서 sample efficiency와 reward bias 를 해결하는 것에 의의를 둔 논문이라고 할 수 있겠다.  

1) Sample efficiency는 기존 off-policy를 사용함으로써 제고하였다.  
2) Reward bias는 Episodic Environment, 즉 Terminal 시점이 존재하는 환경에 한하여 terminal state를 absorbing state로 간주하여 bias를 제고하였다.  
_(absorbing state란 p(s,s) = 1 인, 즉 모든 action에 대해 계속해서 동일한 state가 나오는 state를 의미한다)_


<br>
#### 2. 주관적인 논문 해석  

크게 색다른 것이 없는 논문이라는 느낌을 받았다.  
결국은 기존 Imitation learning에서 off-policy를 적용한 것이고, terminal point에서 추가적인 값을 준 것이라고 느꼈다.  


<br>
#### 3. 나는 왜 별 내용이 없다고 느꼈나

나의 실력이 부족해서 모든 내용을 이해하지 못한 것이 가장 큰 요인일 것이다.
그럼에도 찾아보자면  
1) Sample efficiency를 높이기 위한 목적으로 off-policy를 사용하는 것은 어떻게 보면 너무나 당연한 것이 되었다.  
2) 논문에서 제시한 Reward bias를 해결한 방법은 Imitation learning 뿐 아니라 강화학습 전반에 걸쳐 사용할 수 있으므로 어느정도 유용하게 느껴졌다.  
  개인적으로 다른 강화학습 알고리즘을 구현할 때도 Terminal state를 처리하는 것이 모호하다고 느꼈는데, 적용해볼 수 있을 것이다.  
  그러나 과연 논문에서 제시하는 방법처럼 terminal state를 처리해주는 것이 옳은지에 대한 의문이 남는다.  


<br>
#### 4. 코드 해석

Imitation learning이 모두 그런지 모르겠으나, Discriminator Actor Critic은 아래처럼 구현되어 있다.  

$$
Let \; RL \; be \; a \; initialized \; reinfocement \; learning \; algorithm
$$

$$
1. \; Sample \; from \; RL \\
\quad Sample \; from \; RL \; by \; interacting \; with \; non-reward \; Environment
$$

$$
2. \; Update \; discriminator \\
\quad Update \; discriminator \; network \; by \; input \; expert \; samples \; as \; real \; samples \; and \; input \; RL \; samples \; as \; fake \; samples
$$

$$
3. \; Update \; RL \\
\quad Consider \; discriminator \; score \; as \; a \; reward \; and \; update \; RL
$$

$$
4. \; GOTO \; 1. \; again
$$

이렇게 보면 정말 별거 없다. reward를 discriminator의 score로 주고, discriminator를 업데이트한다. 그 외에는 다른 강화학습과 다를 것이 없다.  


<br>
#### 5. 조금 더 구체적인 코드 설명  
1) discriminator는 wgan-gp에 기반하여 만들어졌다.  
2) rl 알고리즘은 td3 또는 ddpg로 구현되어 있다.  
3) kernel intializer로 orthogonal initializer를 사용했다.  


<br>
#### 6. 왜 하필 WGAP-GP이고 TD3인가  
왜 하필 WGAN-GP를 쓰고, TD3를 썼을까.  
첫째로 WGAN-GP를 쓴 이유는 WGAN-GP가 Generator와 Discriminator의 학습 정도가 불균형해도 결국은 학습이 잘 이뤄지는 특성 때문이라고 생각한다.  
GAN의 관점에서 봤을 때 RL 알고리즘이 결국 Generator의 역할을 대체하는 것이기 때문에,  
RL알고리즘이 잘 학습되지 않은 상태로 Discriminator만 학습된다면 영영 학습되지 않는 불상사가 발생할 수 있다.  
이를 방지하기 위해 WGAN-GP를 사용했다고 본다.  
둘째로 TD3를 쓴 이유는 높은 varinace를 견디기 위해서라고 생각한다.  
Discriminator가 학습이 된다는 이야기는 계속해서 reward가 바뀐다는 것과 같다.  
따라서 필연적으로 variance가 클 수 밖에 없다. 거기에다 off-policy 역시 variance가 크다.  
따라서 variance에 강한, 또는 안전장치가 존재하는 알고리즘이 필요하다.  
그래서 Double Q와 Target network를 갖는 TD3를 사용하지 않았을까 추측한다.  
