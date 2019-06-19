---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 05
---

이번 글에서는 e-greedy 알고리즘 외에 다른 탐색 방법을 알아보고자 한다.  

1. Optimistic Initial Values  
이름에서부터 드러나듯이 보상함수 값에 대한 초기값을 낙관적(큰 양수) 로 설정하는 것이다.  
이후 action은 greedy action 만을 선택한다.  
높은 초기값을 설정했으므로 action을 취하게 되면 해당 action에 대한 기대값이 낮아진다.  
즉, 해당 action은 greedy action이 아니게 되므로 다음에 action을 취할 떄는 다른 action을 취한다.  
이렇게 탐색을 진행하는 방법을 Optimistic Initial Values 방법이라고 한다.  


2. Upper-Confidence-Bound Action Selection  
이 방법은 뽑히지 않은 행동에 대하여 가중치를 부여해 action을 선택하는 방법이다.  
수식적으로 다음의 방법을 따른다.(또는 맥락을 같이하는 방법을 따른다.)  

$$
Let \; c > 0 \\
N(a): \text{a가 뽑힌 횟수} \\
t: \text{전체 횟수, 즉} \quad t = \sum N(a) \\
\\
Action = \underset{a}{argmax} \left(q(a) + c \cdot \sqrt{\frac{\log \; t}{N(a)}} \right)
$$  

c가 크면 어떤 액션의 추정된 보상값이 작더라도, 뽑힌 횟수가 적으면 높은 보정치로 인해 선택될 수 있다.  
즉 explore vs exploit 의 trade-off 관점에서 보았을 때, c가 크면 explore에 더 비중을 둔다고 볼 수 있다.
