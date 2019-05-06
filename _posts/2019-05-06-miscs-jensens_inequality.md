---
layout: post
topic: miscs
title: 젠센 부등식
---
$$
\phi \; is \; convex \\
then,\; \phi(E(X)) \le E(\phi(X)) \; holds. \\
proof) \\
\text{We will use a mathmathical induction.} \\
if \; n = 1, \; trivially \; equailty \; holds. \\
Assume \; this \; inequality \; holds \; for \; n = k \\
Then \; \phi(E(X)) \le E(\phi(X)) \; holds \; where \; X = \{(x_i,\; p_i) | 1 \le i \le k\} \\
Let \; X' = \{(x'_i,\; p'_i) | 1 \le i \le k+1\} \;
s.t. \; p'_i : p'_j = p_i : p_j \; for \; all \; 1 \le i,j \le k \; and \; x_i = x'_i\\
Then \; \phi(E(X')) = \phi(\sum_{i=1}^{k+1} x'_i p'_i) = \phi(x'_{k+1} p'_{k+1} + \sum_{i=1}^{k} x'_i p'_i) = \phi(x'_{k+1} p'_{k+1} + (1 - p'_{k+1})\sum_{i=1}^{k} x_i p_i) \\
\text{By the definition of convexity,} \\
\phi(x'_{k+1} p'_{k+1} + (1 - p'_{k+1})\sum_{i=1}^{k} x_i p_i) \le
p'_{k+1}\phi(x'_{k+1}) + (1 - p'_{k+1})\phi(\sum_{i=1}^{k} x_i p_i) \\
But\; we've \; assumed \; that \; \phi(\sum_{i=1}^{k} x_i p_i) \le \sum_{i=1}^{k} \phi(x_i) p_i \\
So, \; \phi(E(X')) \le E(\phi(X')) \; holds. \\
Thus, \; in \; general \; \phi(E(X)) \le E(\phi(X)) \; holds \; if \; X \; is \; discrete. \\
\text{(generally it holds for continuous cases)}
$$
