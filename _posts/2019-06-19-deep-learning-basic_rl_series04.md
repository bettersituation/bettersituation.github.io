---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 04
---

지난 글에서는 e-greedy 알고리즘에 대해 알아보았다.  
추정함수 q를 아래와 같이 추정했었다.  

$$
\overset{\sim}{q_t}(a) = \frac{\underset{t=1 \sim n}{\sum} R_t \cdot 1_{A_t=a}}
{\underset{t=1 \sim n}{\sum} 1_{A_t=a}}
$$

즉, 단순 평균으로 q를 추정했다.  
그러나 단순 평균이 아니라 지수평균으로 q를 추정할 수도 있다.  


실제로 지수 평균으로 추정하는 것이 non-stationary 문제에는 보다 적합하다.  
그러나 지수 평균을 사용하면 수렴을 보장할 수 없다.  


이 딜레마도 결국은 bias 와 variance 의 trade-off 로 귀결되는 것이다.  
지수 평균을 사용하면 bias 가 증가하나 variance 가 감소하여 빠른 학습을 추구할 수 있다.  

단순 평균을 사용하면 bias 가 감소하나 variance 가 증가하여 수렴 속도는 더뎌지나,  
보다 높은 성능을 기대할 수 있다. (높은 variance 를 극복하여 수렴할 수 있다면)
