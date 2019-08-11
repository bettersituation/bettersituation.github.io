---
layout: post
topic: deep-learning
title: 주관적인 논문리뷰 - Maxout Networks - Ian J. Goodfellow
---
[실제 논문은 여기로](https://arxiv.org/pdf/1302.4389.pdf)  

<br>
#### 1. 대략적인 논문 설명  

2013년도에 작성된 논문이다. 그래서 그런지 Fancy한 느낌을 받지 못했다.  
그렇지만 반대로 뉴럴 네트워크의 기초를 다지고 시야를 넓히는 데에 좋다고 느꼈다.  

간단하게 설명하여, 이 논문은 새로운 activation 방법인 maxout을 제시한 논문이다.  
maxout은 다음과 같다.  

$$
maxout_k(x) = max \left\{A_ix + b_i |i=1 \sim k\right\}
$$

논문에서는 dropout과 maxout의 조합에 대하여 얘기하고,  
relu에 비교하여 maxout의 장점이 무엇인지 얘기한다.  
또한 Universal approximator 임을 증명하였다.  

<br>

#### 2. Dropout과 Maxout의 조합  

Dropout은 학습 시에 랜덤으로 특정 노드 값을 무시하는 학습 방법을 말한다.  
따라서 일종의 Bagging model이라고 볼 수 있을 것이다.  
이 논문에서는 Dropout은 좋은 모델이지만, maxout을 사용함으로써 더 발전시킬 수 있다고 주장한다.  
이는 maxout의 식을 보면 알 수 있다.  
maxout은 k개의 affine values 중 오직 하나만을 취하므로, 다른 affine values가 무시되는 것이 dropout과 닮았다.  
차이는 dropout은 랜덤이라는 것이고, maxout은 확정적이라는 것이다.  
이러한 maxout의 특성이 불안정한 학습 과정을 겪는 dropout을 보완하여 보다 원활한 학습을 이룰 수 있다고 주장한다.  

<br>

#### 3. Relu와의 비교  

Relu는 0이하의 값에서 gradient가 전달되지 않는 dying relu라는 단점이 존재한다.  
반면 maxout은 값에 상관없이 gradient가 전달되는 특징이 존재한다.  
따라서 gradient가 더 잘 전달되어 원활한 학습을 가능하게 한다.  
이러한 차이는 더 깊게 layer를 쌓았을 때 도드라진다.  

또한 training epoch마다 +/- 부호가 바뀌는 비율을 보면,  
maxout은 + &rightarrow; - 로 변하는 비율과 - &rightarrow; + 로 변하는 비율에서 큰 차이가 없다.  

반면 relu는 + &rightarrow; 0 으로 변하는 비율이 0 &rightarrow; + 로 변하는 비율보다 월등히 크다.  
즉, 어떻게 보면 학습이 균형적으로 이뤄지지 않는다고 볼 수 있다.  
또한 0이 많아질수록 dying relu 문제가 도드라질 것이다.  

<br>

#### 4. Universal approximator

Stone-Weierstrass theorem의 내용은 다음과 같다.  

$$
If \; X \; is \; any \; compact \; space, \\
let \; A \; be \; a \; subalgebra \; of \; the \; algebra \; C(X) \; over \; the \; reals \;R \; with \; binary \; operations \; + \; and \; ×. \\
Then, \; if \; A \; contains \; the \; constant \; functions \; and \; separates \; the \; points \; of \; X, \\
A \; is \; dense \; in \; C(X) \; equipped \; with \; the \; uniform \; norm.
$$

실수의 닫힌 공간에 한정하여 설명하면,  
닫힌 구간 위에서 정의된 어떤 연속함수의 집합이 특정 조건을 만족하면,  
닫힌 구간 위에서 정의된 모든 연속함수를 근사할 수 있다는 내용이다.  
(테일러 급수와 푸리에 급수가 대표적인 예시)  

maxout 역시 해당 조건을 충족하여 닫힌 구간 위에서 모든 연속함수를 근사할 수 있음을 증명했다.  


<br>

#### 5. 다른 사람들의 포스팅에 덧붙여  

논문을 읽고, 다른 사람들이 포스팅한 내용도 읽어보았다.  
많은 사람들이 maxout의 sparsity를 중심에 두고 설명함을 알 수 있었다.  
각 포스팅마다 표현은 다를지라도 결국 의미하고 주장하는 것은 ensemble model을 사용하여 성능이 좋아졌다는 것이다.  

나는 여기에 더하여 gradient와 representation 에 대한 내용도 얘기하고자 한다.  
maxout은 dying relu처럼 gradient가 전달되지 않는 문제가 매우 적다.  
왜냐면 어떤 값으로 나왔든 affine으로부터 나온 값이기 때문에 gradient가 전달되기 때문이다.  
뉴럴 네트워크에서 layering에 다른 gradient 문제는 고질적인 문제이기 때문에,  
이를 해결한 측면에서 relu보다 좋은 특성을 갖고 있다고 볼 수 있다.  

또한 representation의 특성에 대해서도 얘기해보고자 한다.  
사실 maxout with k=2 는 relu layer 2개를 쌓아서 만들 수 있다.  
일반적으로 k개 만큼의 relu layer를 쌓으면 maxout with k를 만들 수 있다.  
그렇다면 maxout with k=2 대신 relu layer 2개를 쌓으면 되는 것 아닌가 하는 생각이 들지만 사실 그렇지 않다.  

그 이유는 크게  
(1) relu layer 2개를 쌓는 것이 representation이 더 뛰어난 반면,  
(2) backpropagation 측면에서는 좋지 않기 때문이다.  
즉, trade-off 가 있다.  

따라서 실험을 해보지 않는 이상 무엇이 좋다고 말하기는 어려울 것이다.  


<br>

#### 6. 현재 Maxout이 자주 쓰이나?  

relu보다 maxout이 성능적인 측면에서 좋다고 하는데, 현재 우리는 maxout을 자주 사용하고 있지 않다.  
(GAN같은 경우에서 일부 쓰이고 있지만 개인적으로 Ian이 GAN을 발명하여 고착화된 것이라고 생각한다.)  

그 이유가 무엇일까? 그 전에 relu는 이후 elu, relu6 등 많은 파생 activation을 만들어냈다.  
그런데 왜 maxout은 그렇지 못했을까?  

그 이유는 크게 2가지라고 생각한다.  

첫 째로 maxout은 k값에 따라 많은 계산량을 요구한다.  
둘 째로 프레임워크와의 궁합이 좋지 않았다.  
relu같은 element-wise activation은 현재 널리 쓰이는 tensorflow, pytorch 등과의 궁합이 좋다.  
아래는 element-wise activation인 relu와 maxout의 코드 비교 예시이다.  

```
# 1.Relu

x = Layer(input)
x = relu(x)


# 2. Maxout

x = Layer(input)
maxout_candidates = []
for i in range(k):
    x_candidate = Layer(x)
    maxout_candidates.append(x_candidate)
x = max(maxout_candidates)
```

relu를 적용하기 위해서는 한 줄만 필요했는데, maxout에서는 5줄이 필요하다.  
(list comprehensioin을 사용하여 한 줄로 작성할 수도 있지만 복잡해지는건 여전하다)  

이러한 차이는 element-wise activation의 경우 레이어를 거친 후 일괄적으로 적용할 수 있지만,  
element-wise가 아닌 activation의 경우 레이어를 거친 후 일괄적으로 적용할 수 없기 때문이다.  

이러한 차이는 high level api를 쓰면 더 크게 느껴진다.  
따라서 이러한 작은 불편함 때문에 maxout이 잘 쓰이지 않고, 발전되지 못했다고 생각한다.  

<br>

#### 7. relu의 파생 activation  

위에서 설명했던대로, relu는 많은 파생을 낳았다.  
단점이 명확히 존재하는만큼, 단점을 보완하기 위한 파생 activation이 생겨난 것이다.  

gradient의 관점에서 보자면, leaky relu, parametric relu, softplus, elu, selu, gelu 등  
거의 대부분의 activation이 relu의 문제를 해결하기 위해 제안되거나 사용될 수 있다.  
이들은 maxout에 비해 계산량도 적고,  
일반적으로 얘기하기는 어려우나 maxout 만큼이나 성능이 좋다.  

<br>

#### 8. 패러다임을 떠올리며  

maxout은 2013년도에 투고된 논문이다.  
지금과 같은 딥러닝 프레임워크 환경이 구축되지 않았을 때이다.  
maxout이 만약 현재 사용하고 있는 프레임워크와 궁합이 좋았다면,  
딥러닝이 나아가는 방향인 단순함과 scalable과의 궁합이 좋았다면,  
maxout도 많은 파생 activation을 낳지 않았을까 떠올리며 이 글을 마친다.
