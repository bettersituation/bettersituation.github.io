---
layout: post
topic: computer-science
title: C 와 Python 의 부등식(>, <) 비교
---

요즘 틈틈이 C 기초를 공부하고 있는데, C와 Python이 부등식 비교 방식에서 차이가
난다는 것이 흥미로워 글로 남긴다.

---

#### 1. C 에서의 3 < 4 < 5


우선 C 를 먼저 보자. C 에서 3 < 4 라는 부등식의 결과값은 뭘까? 1 이다.

C 에서는 bool 데이터 형식이 존재하지 않아 1(사실은 0이 아닌 값) 이
bool 데이터에서의 True 를 담당한다.

그러면 반대로 3 > 4 라는 부등식의 결과값은 뭘까? 위와 비슷한 이유로 0 이다.

여기서 재밌는 문제가 발생한다. 3 < 4 < 5 의 값은 뭘까?

(3 < 4) && (4 < 5) 가 아니라 3 < 4 < 5 이다. 물론 부등식을 중첩하여 쓰는 것은
실제로는 해서는 안되는 안좋은 습관이겠으나, 작동하니까 궁금해지는건 어쩔 수 없다.

3 < 4 < 5 의 결과값은 1이다. 이 부등식이 성립해서가 아니다. 3 이 4보다 작으므로
1이 되고, 1이 5보다 작으므로 1이 나오는 것이다.

즉, 3 < 4 < 5 &rightarrow; (3 < 4) < 5 &rightarrow; 1 < 5 &rightarrow; 1 이
되는 것이다.

대충 보면 맞는거 같지만 사실 틀리다. 이는 4 < 3 < 5 라는 부등식을 비교해보면 알 수 있다.
4 < 3 < 5 를 위와 마찬가지로 전개해보면

4 < 3 < 5 &rightarrow; (4 < 3) < 5 &rightarrow; 0 < 5 &rightarrow; 1 이라는
결과가 나온다.

어떻게 보면 작동하는 원리 자체는 굉장히 합리적이다. 우리가 C 를 사용할 때 이렇게만
쓰지 않으면 될 뿐이다.

---

#### 2. Python 에서의 3 < 4 < 5


반면 Python 에서는 어떨까? 3 < 4 < 5 를 입력하면 True 를 반환하고, 4 < 3 < 5 를
입력하면 False 를 반환한다.

```
>>> 3 < 4 < 5
True
>>> 4 < 3 < 5
False
```

즉, Python 은 우리가 직관적으로 생각하는 수학적인 부등식 비교를 실제로 수행한다.
이는 파이썬 공식 문서에서도 확인할 수 있다.

[Python Comparison 공식 문서 보기](https://docs.python.org/3/reference/expressions.html#comparisons)

어떻게 이런 작동이 가능할까 궁금해지니까,
dis 라는 기본 내장 모듈을 사용하여 대략적으로나마 확인해보자.

```
>>> import dis
>>> def multi_compare(a, b, c):
...     return a < b < c
...
>>> dis.dis(multi_compare)
  2           0 LOAD_FAST                0 (a)
              2 LOAD_FAST                1 (b)
              4 DUP_TOP
              6 ROT_THREE
              8 COMPARE_OP               0 (<)
             10 JUMP_IF_FALSE_OR_POP    18
             12 LOAD_FAST                2 (c)
             14 COMPARE_OP               0 (<)
             16 RETURN_VALUE
        >>   18 ROT_TWO
             20 POP_TOP
             22 RETURN_VALUE
>>>
>>>
>>> def and_compare(a, b, c):
...     return a < b and b < c
...
>>> dis.dis(and_compare)
  2           0 LOAD_FAST                0 (a)
              2 LOAD_FAST                1 (b)
              4 COMPARE_OP               0 (<)
              6 JUMP_IF_FALSE_OR_POP    14
              8 LOAD_FAST                1 (b)
             10 LOAD_FAST                2 (c)
             12 COMPARE_OP               0 (<)
        >>   14 RETURN_VALUE
```

코드의 작동 순서도를 보면 알 수 있듯이,
a < b < c 와 a < b and b < c 는 다르게 동작한다.

여기서 주의해서 봐야할 것은 JUMP_IF_FALSE_OR_POP 이 아닐까 한다.
False 면 다음으로 넘어가고, 아니면 POP 을 하겠다는 것인데, 무엇을 POP 하는지가 중요하다.

a < b < c 의 경우 False 일 경우 다음 구문으로 넘어갈 것이고 아니라면 POP 을 할텐데,
JUMP_IF_FALSE_OR_POP 이후 파라메터 b 를 새로 불러오는 것이 없는 것으로 보아 b 를 POP 하는 것을 알 수 있다.

반면 a < b and b < c 의 경우 만약 a < b 가 True 라면 JUMP_IF_FALSE_OR_POP 에서 True를 POP 할 것이다.

즉 Python 에서는 앞 부등식이 False 일 경우 해당 구문은 False 를 반환하며 종료되고, True 일 경우 가장 최근 파라메터를 POP 하여 부등식을 이어나감을 알 수 있다.

그렇다면 한가지 궁금증이 생긴다. 3 < 4 < 5 와 3 < 4 and 4 < 5 중 어떤게 더 빠를까?  100% 신뢰하기는 어려우나 timeit 모듈을 사용하여 대충 한 번 비교해보자.

```
>>> import timeit
>>> timeit.timeit('3 < 4 < 5', number=int(1e8))
5.247673800000001
>>> timeit.timeit('3 < 4 and 4 < 5', number=int(1e8))
4.9094802999999985
>>> timeit.timeit('3 < 4 < 5 < 6', number=int(1e8))
7.4980587999999955
>>> timeit.timeit('3 < 4 and 4 < 5 and 5 < 6', number=int(1e8))
9.753816999999998
>>> timeit.timeit('3 < 4 < 5 < 6 < 7', number=int(1e8))
11.835885099999985
>>> timeit.timeit('3 < 4 and 4 < 5 and 5 < 6 and 6 < 7', number=int(1e8))
9.986279699999983
>>> timeit.timeit('3 < 4 < 5 < 6 < 7 < 8', number=int(1e8))
13.494098699999995
>>> timeit.timeit('3 < 4 and 4 < 5 and 5 < 6 and 6 < 7 and 7 < 8', number=int(1e8))
12.090977400000014
```

결론적으로 봤을 때 잘 모르겠다. and 로 이어주는게 조금 더 빠른거 같기도 하다.
나는 3 < 4 < 5 가 POP 에서 비교될 값을 POP 하므로 조금 더 빠를 줄 알았는데 아니었다.
