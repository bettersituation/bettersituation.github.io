---
layout: post
topic: miscs
title: 젠센 부등식을 활용한 평균 부등식 증명
---
$$
\text{1. 산술평균} \ge \text{기하평균} \\
Let \; \phi(x) = -\;log\; x \; then \; \phi \; is \; convex. \\
Let \; X = \{(x_i,p_i)|1 \le i \le k,\; x_i > 0, \; p_i = \frac{1}{k}\} \\
then, \; E(\phi(X)) = -log(\prod_{i=1}^k x_i^{\frac{1}{k}}) \; and \;
\phi(E(X)) = -log(\frac{\sum_{i=1}^k x_i}{k}) \\
Thus, \; -log(\frac{\sum_{i=1}^k x_i}{k}) \le -log(\prod_{i=1}^k x_i^{\frac{1}{k}}) \; holds. \\
or \; equivalently, \\
\frac{\sum_{i=1}^k x_i}{k} \ge \prod_{i=1}^k x_i^{\frac{1}{k}} \; holds. \\
\text{ }\\
\text{ }\\
\text{2. 기하평균} \ge \text{조화평균} \\
\text{In the case of 1, we can assume} \; x_i = \frac{1}{a_i} \\
then, \; \frac{\sum_{i=1}^k x_i}{k} = \frac{\sum_{i=1}^k \frac{1}{a_i}}{k} \; and \;
\prod_{i=1}^k x_i^{\frac{1}{k}} = \prod_{i=1}^k (\frac{1}{a_i})^{\frac{1}{k}} \\
thus, \; \frac{k}{\sum_{i=1}^k \frac{1}{a_i}} \le \prod_{i=1}^k{a_i}^{\frac{1}{k}} \; holds.
$$
