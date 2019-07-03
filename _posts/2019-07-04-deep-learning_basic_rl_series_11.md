---
layout: post
topic: deep-learning
title: 강화학습 기초 시리즈 11
---

<h4>Monte Carlo</h4>
<br>

기대 보상합 추정하고 policy를 업데이트 하기 위하여 Dynamic Programming 방법론을 사용하는 것처럼  
몬테카를로 방법론을 사용하여 가치를 추정하고, policy를 업데이트할 수 있다.  
가치를 추정하기 전에 하나 짚고 넘어가야 하는 것이 있다.

<br>
<br>
**First visit vs Every visit**  
환경과 상호작용하다보면 한 trajectory 내에서 특정 환경 상태(state) 가 반복적으로 나타날 수 있다.  
기대 보상합을 추정하기 위하여 해당 state의 정보를 사용할 때  
*처음 발생한 state* 만 사용할지, *반복적으로 발생한 모든 state* 를 사용할지 정해야 한다.  
처음 발생한 state만 사용한다면, 즉 first visit 이라면 기대 보상합 추정은 아래 과정처럼 나타난다.  

$$
Let \; policy \; \pi \; is \; given, \\
return_s \; is \; a \; list \; to \; save \; rewards
$$

$$
Repeat \; forever\\
\quad generate \; a \; trajectory \; using \; \pi \\
\quad for \; each \; state \; s \; in \; trajectory: \\
\quad \quad G \leftarrow the \; sum \; of \; rewards \; that
\; follows \; the \; first \; occurance \; of \; s \\
\quad \quad append \; G \; to \; return_s \\
\quad \quad v(s) \leftarrow Average \; of \; return_s \\
$$  

만약 every visit 을 사용한다면 모든 visit 에 대하여 보상합의 평균을 구해주면 된다.
