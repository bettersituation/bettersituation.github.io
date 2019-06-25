---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 09
---

<h4>벨만 등식과 벨만 최적 등식</h4>
<br>

**1. 벨만 등식**  
벨만 등식이란 다음 등식을 뜻한다.  

$$
v_{\pi}(s) = E(G_t|S_t=s) = \int \pi(a|s) \cdot \left(\int p(s',r|s,a) \cdot  \left(r + \gamma v_{\pi}(s')\right) \right)
$$  
<br>

**2. Optimal policy**  
Optimal policy란 해당 policy를 따라 action을 취했을 때,  
다른 어떤 policy를 따라 action을 취하는 것보다 큰 보상 합계를 기대할 수 있는 policy를 뜻한다.  
참고로 Optimal policy는 유일하지 않을 수 있다.  

$$
If \; \pi_* \; is \; an \; optiaml \; policy, \\
v_{\pi_*}(s) \ge v_{\pi}(s) \; holds \; for \; any \; \pi, \; s.
$$
<br>

**3. 벨만 최적 등식 v**  
Value of state는 optimal policy에 대하여 다음이 성립한다. 이를 벨만 최적 등식이라고 한다.  

$$
v_{\pi_*}(s) = \underset{a}{max} \; q_{\pi_*}(s, a) = \underset{a}{max} \int p(s',r|s,a) \cdot (r + \gamma v_{\pi_*}(s')) = \underset{a}{max} \left[r(s,a) + \gamma \int p(s'|s,a) \cdot v_{\pi_*}(s') \right]
$$  
<br>

**4. 벨만 최적 등식 q**  
q는 optimal policy에 대하여 다음이 성립한다. 이 역시 벨만 최적 등식이라고 표현한다.

$$
q_{\pi_*}(s,a) = E(G_t|S_t=s, A_t=a) = \int p(s',r|s,a) \cdot (r + \gamma v_{\pi_*}(s')) = r(s,a) + \gamma \int p(s'|s,a) \cdot \underset{a}{max} \; q_{\pi_*}(s', a)
$$  
