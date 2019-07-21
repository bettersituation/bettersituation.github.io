---
layout: post
topic: finance
title: cfa lv1 quant reading 05
---

<h4>Common Probability Distributions</h4>
<br>

**Definitions**  
(1) Discrete / Continuous random variable  
(2) Probability function  
(3) pmf / pdf / cdf  


<br>
**Distributions**  
(1) discrete uniform  
(2) bernoulli (E=p, V=pq)   
(3) binomial (E=np, V=np(1-p))  
(4) continuous uniform  
(5) normal (standard normal)  
(6) multivariate distribution  
(7) multivariate normal  
(8) lognormal  
$$ e^X \; where \; X \sim N(\mu, \sigma^2) $$


<br>
**Safety-First Criterion and Shortfall risk**  

$$
SFRatio = \frac{E(R_p) - R_L}{\sigma_p} \\
Shortfall \; risk = P(R_p < R_L) = P(Z < SFRatio)
$$


<br>
**Continuous compounding rate**  

$$
EAR = e^{r_{cc}} - 1 \\
\ln \frac{S_1}{S_0} = \ln(1 + HPR) = r_{cc}
$$


<br>
**Monte Carlo simulation**  
- Process  
(1) Specify distributions followed by other factors  
(2) Randomly generate factors  
(3) Valuing stats of target distributions for each randomly generated factors  
(4) Calculate desired stats  
- Limitation  
(1) complex and assumption of distributions and factor relations  
(2) no insight  


<br>
**Historical simulation**  
- Process  
(1) Collect historical data  
(2) Randomly select value from collected data  
- Advantage  
(1) No assumption  
- Limitation  
(1) Past changes may not be a good estimator  
(2) Infrequent events  
(3) Cannot explain unoccured events  
