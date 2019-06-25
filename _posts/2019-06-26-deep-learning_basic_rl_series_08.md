---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 08
---

지난 글에 이어 강화학습의 기초 개념에 대해 소개한다.  

**1. Discounting Factor**  
미래에 받을 것으로 예상되는 보상의 할인 합계를 위해서 사용되는 Factor이다.  
에피소드 환경처럼 정해진 종료 시점이 있는 경우는 문제되지 않으나,  
종료시점이 없는 환경인 경우 보상 합계를 수렴시켜주기 위해 Discounting Factor는 1 미만이어야 한다.  

$$
0 \le \gamma \le 1 \; , \\
G_t := \underset{a \sim \pi}{E}\left(\sum_t \gamma^t \cdot r(s_t) \right)
$$
<br>

**2. Value of state**  
value of state란 주어진 state에서 Agent가  
policy(또는 preference)를 따라 action을 취했을 때 기대되는 보상 합계이다.  

$$
v_{\pi}(s) = E(G_t|S_t=s)
$$  
<br>

**3. Q**  
Q란 주어진 state에서 Agent가 특정 action을 취했을 때에 기대되는 보상 합계이다.  

$$
q_{\pi}(s,a) = E(G_t|S_t=s,A_t=a) = r(s,a) + \gamma \cdot E(G_{t+1})
$$
<br>
