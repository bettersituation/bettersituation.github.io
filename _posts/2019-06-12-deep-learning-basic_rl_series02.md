---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 02
---

강화학습에 대한 기본 컨셉은 간단하다.  
“**어떤 행동을 취할 때 얼만큼의 보상을 받는가? 그래서 어떤 행동을 해야 좋은가?**”  

강화학습이라는 것은 결국 “행동에 대한 보상” 을 푸는 것이다. 이 때, 어떤 행동에 대한 추정된 보상값이 아닌 참으로서의 보상값이 있을 것이다. 이를 수식으로 표현하기 위해 아래와 같은 기호를 먼저 정의하자.

$$
a: \text{선택 가능한 해동} \\
A_t: \text{t번째에 선택한 행동} \\
R_t: \text{t번째에 선택한 행동으로 인해 받은 보상값 분포}
$$


위와 같이 기호를 정의했을 때, t번 째 상황에서 a라는 행동을 선택했을 때 받을 수 있는 보상에 대한 기대값은 아래와 같은 조건부 기대값으로 표현된다.  

$$
q_*(a) = E(R_t|A_t=a)
$$

해당 식의 좌변에는 시점 t에 대한 정보가 없다. 즉 시점 t에 상관없이 어떤 행동에 대하여 평균적으로 같은 보상을 기대할 수 있음을 의미한다. 이러한 상황을 stationary 하다고 한다.  

이 때, a가 취할 수 있는 행동의 개수에 따라 k-armed bandit 이라고 표현한다. 예를 들어 취할 수 있는 행동이 4개 뿐인 stationary 문제는 4-armed bandit 이라고 표현된다.  

사실 어떤 행동이 가장 큰 보상을 주는가를 표현하는 q 함수를 알면 강화학습은 할 필요가 없다. 그러나 우리는 q를 모르기 때문에 다양한 방법을 통해 추정하고, 여기에서 강화학습이 시작된다.  
