---
layout: post
topic: finance
title: cfa lv1 quant reading 04
---

<h4>Probability Concepts</h4>
<br>

**Definitions**  
(1) Random variable  
(2) Outcome / Event    
(3) Mutually exclusive  
(4) Exhaustive  

$$  
if \; S \subset U, \; 0 \le P(S) \le 1 \; holds \\
if \; \left\{S_i \subset U \right \} \; are \; mutually \; exclusive \; and \; exhaustive, \sum P(S_i) = 1
$$    

<br>
**Formulars**  

$$
P(AB) = P(A|B) * P(B) \\
P(A \; or \; B) = P(A) + P(B) - P(AB) \\
P(A) = \sum P(A|B_i) * P(B_i) \; if \; \left\{B_i\right\} \; are \; mutually \; exclusive
$$


<br>
**Concepts**  

$$
If \; P(A|B) = P(A) \; holds, \; A \; and \; B \; are \; called \; independent \\
E(X) = \sum x_i * P(x_i) \\
Cov(X, Y) = E[(X - E(X))(Y - E(Y))] = E(XY) - E(X)E(Y) \\
Cov(X, X) = Var(X) \\
Corr(X, Y) = \frac{Cov(X, Y)}{\sigma(X)\sigma(Y)} \; where \; \sigma(X)^2 = Var(X) \\
-1 \le Corr(X, Y) \le +1 \; holds
$$


<br>
**Bayes formular**  

$$
P(A|B) = P(B|A) * \frac{P(A)}{P(B)}
$$


<br>
**Combination and Permutation**  

$$
{}_nC_r = \frac{n!}{r!(n-r)!} \\
{}_nP_r = \frac{n!}{(n-r)!}
$$
