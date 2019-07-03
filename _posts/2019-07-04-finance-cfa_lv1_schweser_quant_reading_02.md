---
layout: post
topic: finance
title: cfa lv1 quant reading 02
---

<h4>Cash Flow applications</h4>
<br>

**Concepts**  
(1) NPV  
(2) IRR  
(3) HPR(Holding Period Return) = (ending - beginning) / beginning  


**Money-weighted return**  
is an application of IRR  


**Time-weighted return**  
geometric average of each periodic returns  
```
ex) buy a stock for $10 at year0,  
buy a stock onemore for $8 at year1, dividend paid $1,  
sell 2 stocks for 12 for year2, no dividend paid.  
```
```
sol)
HPY1 = (8 + 1) / 10 - 1 = -10%  
HPY2 = 24 / 16 - 1 = 50%  
Time-weighted return = sqrt(0.9 * 1.5) - 1 = 16.19%
```


**Bank discount yield**  
$$
r_{BD} = \frac{Difference}{Face \; value} \times \frac{360}{t}
$$


**HPY(Holding period yield) or HPR**  
$$
HPY = \frac{P_1 + D - P_0}{P_0}
$$

**EAY(Effective annual yield)**  
$$
EAY = (1 + HPY)^{\frac{365}{t}} - 1
$$

**Money market yield(or CD equivalent yield)**  
$$
r_{MM} = HPY \times \frac{360}{t} \; \\
or \; equivalently, \\
r_{MM} = \frac{360 - r_{BD}}{360 - t \cdot r_{BD}}
$$

**Bond equivalent yield**  
$$
bond \; equivalent \; yield = 2 \times  (\sqrt{1 + EAY} - 1)
$$
