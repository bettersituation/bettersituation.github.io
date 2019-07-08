---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 12
---

<h4>Monte Carlo 두번째</h4>
<br>

강화학습은 결국 Exploration과 Exploitation의 trade off라고 할 수 있다.  
몬테카를로 역시 Exploration이 중요하다. 따라서 Exploration을 보장해주기 위해 두가지 방법을 사용한다.  

<br>

**Exploration start**  
Exploration start린 처음 주어지는 state에서 취할 수 있는 모든 action의 확률이 양수임을 보장하는 것이다.  
이렇게 함으로써 모든 행동에 대한 Exploration을 할 수 있다.  


<br>

**e-soft policy**  
다음의 성질을 만족할 때 e-soft policy라고 부른다.  

$$
\forall a \in A(s) \quad  \pi(a|s) \ge \frac{\epsilon}{|A(s)|}
$$

모든 action의 확률이 양수임을 보다 엄격하게 제한한 것이라고 볼 수 있다.  
