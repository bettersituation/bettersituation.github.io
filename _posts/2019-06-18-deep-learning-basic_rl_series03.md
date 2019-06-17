---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 03
---

강화학습이란 결국 행동에 대한 보상 함수인 q를 추정하는 것이다.  
이번 글에서는 q 를 추정하는 방법 중 하나인 e-greedy 알고리즘을 소개한다.  

k-armed bandit 문제에서 q를 추정하는 가장 간단한 방법은 무엇일까?  
아마도 행동을 취하고, 얻게된 보상을 기록하여 분포를 추정하는 것일 것이다.  
식으로 표현하면 아래와 같다.  

$$
A_t: \text{t번 째에 취한 행동} \\
R_t: \text{t번 째에 얻은 보상} \\
\\
1_{A_t=a} =
\begin{cases}
1 & if \; A_t = a \\
0 & if \; A_t \neq a
\end{cases} \\
\\
q(a) \sim Distribution(R_t|A_t=a)
$$

그러나 분포를 직접 추정하기는 어려우므로 분포를 대신할 수 있는 값인 평균을 사용하여
분포를 대체한다.  
$$
q(a) = \frac{\sum R_t \cdot 1_{A_t=a}}{\sum{1_{A_t=a}}}
$$

이렇게 q를 정의하고 나면 e-greedy 알고리즘을 구현할 수 있다.  
그전에 greedy 란 무엇일까? greedy 란 '탐욕적인' 것을 뜻하는데,  
이 경우에는 가장 높은 보상을 갖는 행동을 말한다. (즉 greedy한 action을 의미한다.)  
$$
Greedy \; action = Argmax \; q(a)
$$

우리가 greedy action 만을 선택할 수 있다면 좋을 것이다. 그러나 우리는 참으로서의 q는 알지 못하고, q를 추정할 뿐이다.  
따라서 오차가 존재할 수 밖에 없고, 이를 보완해주기 위해서는 greedy action 이 아닌 행동에 대한 정보도 수집해야 한다.  
여기서 e-greedy 알고리즘이 등장한다.  

e-greedy 알고리즘이란 결국 greedy action 과 랜덤 action 을 적절한 비율로 선택하여  
높은 보상을 얻으며 추정 오차를 수정하는 알고리즘이다.  

$$
Let \; 0 < e < 1 \\
P(A_t = greedy \; action) = 1 - e \\
P(A_t \neq greedy \; action) = e
$$

e-greedy 알고리즘에서는 위 확률로 행동을 선택한다.  

사실 이러한 trade-off 는 모든 문제에서 등장한다.  
bias vs variance 와 마찬가지로 강화학습에서는 exploit 과 explore 가 trade-off 관계에 있다.  
exploit 이란 현재 주어진 정보 내에서 가장 적합한 행동을 취하는 것이다.  
반면 explore 는 현재 주어진 정보 내에서 적합하지 않은 행동일지라도 해당 행동을 함으로써 추정을 업데이트하는 것이다.  

exploit 만 한다면 최적의 행동을 찾을 수 없다. explore만 한다면 최적의 행동을 취할 수 없다.  

따라서 적절한 exploit 과 explore 를 하는 것은 강화학습의 key point 중 하나이다.
