---
layout: post
topic: miscs
title: 마코브, 체비셰프 부등식
---
#### 1. 마코브 부등식
$$
\text{Assume u is non-negative and c > 0.} \\
then, \; P(u(x) \ge c) \le \frac{E(u(X))}{c} \; holds. \\
proof) \\
E(u(X)) = \int{p(x)u(x)} = \int_{u(x) \ge c}{p(x)u(x)} + \int_{u(x) < c}{p(x)u(x)} \\
\ge c\int_{u(x) \ge c}{p(x)} + \int_{u(x) < c}{p(x)u(x)}
= c \cdot P(u(x) \ge c) + \int_{u(x) < c}{p(x)u(x)}\\
\ge c \cdot P(u(x) \ge c) + 0 = c \cdot P(u(x) \ge c) \\
Thus,\\
E(u(X)) \ge c \cdot P(u(x) \ge c) \\
or\; equivalently, \\
P(u(x) \ge c) \le \frac{E(u(X))}{c} \; holds.
$$

<br><br><br>

#### 2. 체비셰프 부등식
$$
\text{Assume u is a mean of distribution X and s is a standard deviation.} \\
Let\; s \neq 0\; and\; \kappa > 0\\
Then, \\
P(|X-u| \ge \kappa s) \le \frac{1}{\kappa^2} \\
or\; equivalently, \\
P(|X-u| \le \kappa s) \ge 1 - \frac{1}{\kappa^2} \\
proof) \\
Let\; \phi(x) = \frac{(x-u)^2}{\kappa^2 s^2} \\
then \; \phi \ge 0 \; holds\; for \; all\; x \in \mathcal{R} \\
By \; Markov\; Inequality, \\
P(\phi(x) \ge 1) = 1 \cdot P(\phi(x) \ge 1) \le \frac{E(\phi(X))}{1} = E(\phi(X)) \; holds. \\
E(\phi(X)) = E(\frac{(x-u)^2}{\kappa^2 s^2}) = \frac{1}{\kappa^2 s^2} E((x-u)^2) = \frac{1}{\kappa^2 s^2} \cdot s^2 = \frac{1}{\kappa^2} \\
and, \\
P(\phi(x) \ge 1) = P(\frac{(x-u)^2}{\kappa^2 s^2} \ge 1) = P((x-u)^2 \ge \kappa^2 s^2) = P(|x-u| \ge \kappa s) \\
thus, \\
P(|x-u| \ge \kappa s) \le \frac{1}{\kappa^2} \; holds.
$$
