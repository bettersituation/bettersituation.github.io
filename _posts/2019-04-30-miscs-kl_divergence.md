---
layout: post
topic: miscs
title: kl divergence
---
kl divergence 란 두 확률 분포가 얼마나 차이나는지를 측정하는 값 중 하나이다.

정의는 다음과 같다.

$$
\text{Let P, Q are distributions.} \\
\text{Then KL divergence is defined as follows,} \\
D_{KL}(P, Q)= \int{p(x) \log{\frac{p(x)}{q(x)}}}
$$

symmetric 하지 않으므로 metric 은 아니지만 자주 쓰인다.
<br>
<br>

참고)
주요 성질 중 하나는 kl divergence ≥ 0 이 성립한다는 것인데, 이는 아래처럼 Jenson’s inequality 를 활용해 증명할 수 있다. (x 에서 y로 변하는 부분이 엄밀하지 못하지만)
<br>
<br>

$$
\text{Let P, Q are distributions} \\
set \; \phi(x) = x\log x, \; \text{which is convex.} \\
then, \; \int{p(x) \log{\frac{p(x)}{q(x)}}} = \int{q(x) \phi(\frac{p(x)}{q(x)})} = \int{p_Y(y)\phi(y)} \\
\text{where Y is a new distribution s.t.} \\
y = \frac{P(x)}{Q(x)} \; and \; P_Y(y) = Q(x) \\
\\
then, \; by \; Jenson's \; inequality, \\
\int{p_Y(y)\phi(y)} \ge \phi(\int{y \cdot p_Y(y)}) = \phi(\int{\frac{p(x)}{q(x)}q(x)}) = \phi(\int{p(x)}) = \phi(1) = 0 \\
thus, D_KL(P,Q) \ge 0 \; holds.
$$
