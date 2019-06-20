---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 06
---

e-greedy, optimistic initial values, upper-confidence-bound action selection 알고리즘 모두 추정된 보상함수 q에 따라 행동이 직접적으로 결정되었다.  


이번에는 q를 간접적으로 사용하여 행동을 선택하는 방법을 소개한다.  
우선 행동에 대한 선호(preference)를 나타내는 함수 H를 정의한다.  
H에 의해 특정 행동을 선택할 확률이 결정되고, 이러한 H를 업데이트할 때 q를 사용한다.  


H를 정의하는 방법은 다양하겠으나, 대표적으로 아래와 같이 정의할 수 있다.  

$$
Pr(A_t=a) = \pi_t(a) = \frac{e^{H_t(a)}}{\sum e^{H_t(a)}}
$$

H는 q를 사용하여 아래처럼 업데이트할 수 있다.  

$$
Let \; 0 < \alpha  \\
H_{t+1}(A_t) = H_t(A_t) + \alpha \cdot (R(A_t) - \overset{-}{R}) \cdot (1 - \pi_t(A_t)) \\
H_{t+1}(a) = H_t(a) - \alpha \cdot (R(a) - \overset{-}{R}) \cdot \pi_t(a) \; for \; all \; a \neq A_t
$$

즉 선택된 행동에 의해 받은 보상이 평균적인 보상보다 높다면 preference 를 높이고, 낮다면 preference를 낮추는 식으로 H의 업데이트가 진행된다.  

그리고 위 업데이트식은 stochastic approximation에 근간을 두고 있는데, 아래 식으로부터 유도된다.  

$$
H_{t+1}(a) = H_t(a) + \alpha \cdot \frac{\partial E(R_t)}{\partial H_t(a)}
$$
