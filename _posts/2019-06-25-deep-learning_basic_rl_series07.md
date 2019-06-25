---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 07
---

이번 글에서는 강화학습의 기초 개념에 대해 소개한다.  

**1. Agent와 Environment**  
Agent는 행동하는 대상을 의미하고, Environment는 주어진 환경을 의미한다.  
예를 들어 마리오에서 마리오는 Agent, 스테이지 맵은 Environment라고 할 수 있을 것이다.  
이 때 Agent가 직접 통제 가능한 것만을 action이라고 한다.  
<br>

**2. MDP와 Conditional Distributions**  
MDP(Markov Decision Process)란 Agent가 다음에 직면할 state와 reward가 현재의 state 및 action(decision) 에 의해서만 영향을 받는다는 가정입니다.  
MDP를 가정하면 아래처럼 다양한 conditional distributions를 생각해볼 수 있다.  

$$
p(s',r|s,a) = P(S_t=s',R_t=r|S_{t-1}=s,A_{t-1}=a) \\
p(s'|s,a) = \int p(s',r|s,a) \;dr \\
p(r|s,a) = \int p(s',r|s,a) \; ds' \\
r(s,a) = E(r|s,a) = \int r \cdot p(r|s,a) \; dr \\
r(s'|s,a) = E(r|s,a,s') = \frac{\int r \cdot p(s',r|s,a) \; dr}{ p(s'|s,a)}
$$
