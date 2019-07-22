---
layout: post
topic: finance
title: cfa lv1 quant reading 06
---

<h4>Sampling and Estimation</h4>
<br>

**Sampling methods**  
(1) Simple random sampling    
(2) Systematic sampling (every n'th)  
(3) Stratified random sampling  


<br>
**Types of data**  
(1) Time-series data  
(2) Cross-sectional data  
(3) Longitudinal data (time series + cross sectional)  
(4) Panel data  


<br>
**Central limit theorem**  

$$
\text{regardress of it's own distribution,} \\
\underset{n \rightarrow \infty}{\lim} \frac{\overline{X} - \mu}{s_X} = N(0, 1)
$$


<br>
**Standard error of the sample mean**  

$$
stderr_{X, n} = \sigma_{\overline{X}} = \frac{\sigma_X}{\sqrt{n}}
$$


<br>
**Desirable properties of an estimator**  

(1) unbiased (E(f) = k)  
(2) efficient (V(f) &le; V(f') under unbiased)  
(3) consistent (P(|f-k|) < e = 1 as n &rarr; &infin;)  


<br>
**Point estimator and Confidence interval**  



<br>
**Student's t distribution**  

- property) t is flatter than normal  
- degree of freedom is n - 1 where n is a sample size  

|condition|n < 30|n &ge; 30|
|---|---|---|
| normal with known variance | z | z |
| normal with unknown variance | t | t or z |
| non-normal with known variance | X | z |
| non-normal with unknown variance | X | t or z |


<br>
**Confidence interval**  

$$
P(|z| \le 1.645) = 0.90 \\
P(|z| \le 1.960) = 0.95 \\
P(|z| \le 2.575) = 0.99
$$


<br>
**Types of bias**  
(1) Data mining bias (lack of background, overestimate factor)  
(2) Sample selection bias  
(3) Survivorship bias  
(4) Look ahead bias  
(5) Time period bias
