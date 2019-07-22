---
layout: post
topic: finance
title: cfa lv1 quant reading 07
---

<h4>Hypothesis testing</h4>
<br>

**Definitions**  
(1) Null / Alternative hypothesis    
(2) one-tailed / tow-tailed test  
(3) Type 1 error (significance level)  
(4) Type 2 error (power of a test)  

| Decision | Truly H0 | Truly Ha |
| --- | --- | --- |
| not reject H0 | Correct | Type 2 error |
| reject H0 | Type 1 error(significance level) | Correct (Power of a test) |


<br>
**mean differences**  

$$
\text{unknown but assumed equal variances} \\
t = \frac{\overline{X_1} - \overline{X_2}}
{(\frac{s_p^2}{n_1} + \frac{s_p^2}{n_2})^{1/2}}
\; where \; s_p = \frac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2}{n_1 + n_2 - 2}
\; (df = n_1 + n_2 - 2) \\
$$

$$
\text{unknown and assumed not equal variances} \\
t = \frac{\overline{X_1} - \overline{X_2}}
{(\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2})^{1/2}}
\; where \; df = \frac{(\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2})^2}
{\frac{(s_1^2/n_1)^2}{n_1} + \frac{(s_2^2/n_2)^2}{n_2}}
$$

(1) Time-series data  
(2) Cross-sectional data  
(3) Longitudinal data (time series + cross sectional)  
(4) Panel data  


<br>
**Chi-square**  

$$
H_0: \sigma^2 = \sigma_0^2 \quad vs \quad H_a: \sigma^2 \ne \sigma_0^2 \; or \; one-tailed \\
\chi_{n-1}^2 = \frac{(n-1)s^2}{\sigma_0^2}
$$


<br>
**F-distribution**  

$$
H_0: \sigma_1^2 = \sigma_2^2 \quad vs \quad H_a: \sigma_1^2 \ne \sigma_2^2 \; or \; one-tailed \\
F = \frac{s_1^2}{s_2^2}
$$


<br>
**Parametric and Non-parametric test**  

Non-parametric is used when  
(1) The assumptions of distribution are not met  
(2) Data are at most ordinal  
(3) Hypothesis does not involve parameters of the distribution  
ex) Spearman rank correlation is non-parametric test  
