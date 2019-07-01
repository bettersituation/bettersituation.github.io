---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 10
---

<h4>Dynamic Programming</h4>
<br>

Dynamic Programming 이란 특정 알고리즘을 말하는 것이 아니라,  
주어진 문제를 순차적으로 풀어나가는 것을 의미한다.  
Dynamic Programming과 벨만 등식이 어떻게 엮일 수 있는지 알아본다.  

<br>
<br>
**1. Policy Evaluation**  
Policy Evaluation이란 현재 Policy를 따를 때 얻을 수 있는 보상 합에 대한 기대값,  
즉 주어진 policy에 대하여 현재 state의 가치를 추정하는 것을 의미한다.  
Dynamic Programming을 활용하여 가치 함수를 업데이트하는 과정은 아래와 같다.  

$$
Let \; policy \; \pi \; is \; given, \\
and \; \theta \; is \; a \; small \; positive \; number \;
which \; is \; an \; acceptable \; maximum \; error
$$

$$
Initialize \; v(:S \rightarrow R) \; arbitraily \\
Repeat \\
\quad \triangle \leftarrow 0 \\
\quad For \; each \; s \in S: \\
\quad \quad v_s \leftarrow v(s) \\
\quad \quad v(s) \leftarrow \int_{s} p(s',r|s,\pi(s))(r + \gamma v(s')) \\
\quad \quad \triangle \leftarrow max(\triangle, |v_s - v(s)|) \\
until \; \triangle < \theta
$$  

<br>
<br>
**2. Policy Improvement**  
Policy 자체의 성능을 높이기 위해 아래처럼 Dynamic Programming을 사용할 수 있다.  
이 때 업데이트된 poilcy에 대한 가치 추정이 필요하므로 policy improvement를 할 때마다 policy evaluation이 필요하다.  

$$
(1) \; Initialize \; policy \; \pi \; and \; value \; estimator \; v \; arbitraily, \\
and \; set \; acceptable \; maximum \; error \; \theta
$$

$$
(2) \; Policy \; Evaluation
$$

$$
(3) \; Policy \; Improvement \\
policy \; stable \leftarrow \; true \\
for \; each \; s \in S: \\
\quad old \; action \leftarrow \pi(s) \\
\quad \pi(s) \leftarrow \underset{a}{argmax} \int_{s',r} p(s',r|s,a)(r + \gamma v(s')) \\
\quad if \; old \; action \neq \pi(s): \\
\quad \quad policy \; stable \leftarrow false \\
if \; policy \; stable = false: \\
\quad go \; to \; (2)
$$

<br>
<br>
**3. Value Iteration**  
Policy Improvement는 매 업데이트마다 policy evaluation을 수행해야 하므로 효율적이지 않다.  
Value Iteration은 이를 보완한 방법으로, 최적의 value를 추정한 후 value로부터 policy를 추출한다.  

$$
Initialize \; value \; estimator \; v \; arbitraily, \\
and \; set \; acceptable \; maximum \; error \; \theta
$$

$$
Repeat \\
\quad \triangle \leftarrow 0 \\
\quad For \; each \; s \in S: \\
\quad \quad v_s = v(s) \\
\quad \quad v(s) = \underset{a}{max} \int p(s',r|s,a)(r + \gamma v(s')) \\
\quad \quad \triangle \leftarrow max(\triangle, |v_s - v(s)|) \\
until \; \triangle < \theta
$$

$$
set \; \pi \; s.t. \\
\pi(s) = \underset{a}{argmax} \int p(s',r|s,a) (r + \gamma v(s'))
$$
<br>
