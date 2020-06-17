---
layout: post
topic: computer-science
title: PEP8
---

PEP8 은 파이썬 코딩 스타일 가이드이다. [(https://www.python.org/dev/peps/pep-0008/)](https://www.python.org/dev/peps/pep-0008/)  
협업을 위해서 등 여러 이유로 코딩 스타일을 통일하는 것이 좋을 것이다.  
그렇기에 pep8 를 읽고 내용을 간단하게 요약해본다.  

---
  
#### Indentation

1. Indentation 은 4 spaces 로 구성한다.  
2. 코드가 이어지는 경우 위의 줄과 align 한다.  
```pydocstring
foo = long_function_name(var_one, var_two,
                            var_three, var_four)
```
3. Hanging Indents 의 경우 첫 줄에는 아무 인자도 받지 않으며, 들여쓰기 한다.
```pydocstring
foo = long_function_name(
       var_one, var_two,
       var_three, var_four)
```
4. 마지막 bracket 의 경우 함수 인자나 list 등에서 추가적인 line 의 첫 위치에 쓸 수도 있고, 들여쓰기 후 쓸 수도 있다.
```pydocstring
my_list = [
       1, 2, 3,
       4, 5, 6,
]
result = some_function_that_takes_arguments(
       'a', 'b', 'c',
       'd', 'e', 'f',
       )
```

---

#### Line

1. 한 줄의 길이를 최대 79 자, 주석 및 docstring 의 경우 72 자로 제한한다.
2. 긴 줄의 경우 백슬래시(\) 로 line-breaking 하여 사용한다.
```pydocstring
with open('/path/to/some/file/you/want/to/read') as file_1, \
        open('/path/to/some/file/being/written', 'w') as file_2:
       file_2.write(file_1.read())
```
3. 여러 줄에 걸친 binary 연산의 경우 연산자가 앞에 오도록 한다.
```pydocstring
income = (gross_wages
             + taxable_interest
             + (dividends - qualified_dividends)
```
4. 함수와 클래스는 위로 두 줄의 blank line 을 갖는다.
5. 클래스 내부 함수 등에서는 위로 한 줄의 blank line 을 갖는다.
6. 함수 내부 코드 등에서 논리 상 구분을 위해 blank line 을 사용한다.

---

#### Imports

1. 하나의 import 문에서는 하나의 모듈만 import 한다.  
2. from A import B, C 등은 허용한다.
3. import 는 파일 주석과 docstrings 밑에서 수행한다. import 이후 global variable 과 constant 등을 정의한다.
4. 절대경로 import 가 선호된다.
5. from A import * 처럼 wildcard(*) 의 사용은 되도록 피한다.
6. dunders (ex. \_\_all\_\_ 등) 의 정의는 import 이전에 수행한다. 단 from \_\_futures\_\_ import 는 dunders 이전에 수행한다.

---

#### String Quotes

1. 따옴표이든 쌍따옴표이든 하나를 convention 으로 정하여 고수하면 된다.
2. multi-line string 을 위한 triple quote 의 경우 docstring 과의 일관성을 위해 쌍따옴표를 사용한다.

---

#### Whitespace in Expressions and Statements

1. 개괄호 직후 및 폐괄호 직전에 space 를 사용하지 않는다.  
```pydocstring
spam(ham[1], {eggs: 2})
```
2. trailing comma 와 폐괄호 사이를 띄어쓰지 않는다.
```pydocstring
foo = (0,)
```
3. if statement 등의 콜론(:) 직전에 띄어쓰지 않는다.
4. 다만 slicing 에서는 콜론(:) 양쪽에 인자가 있을 경우 양쪽 모두를 띄어서 쓸 수도 있다. 이 때의 콜론은 연산자와 동등하게 대우될 수 있기 때문이다.
```pydocstring
ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
ham[lower:upper], ham[lower:upper:], ham[lower::step]
ham[lower+offset : upper+offset]
ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
ham[lower + offset : upper + offset]
```
5. 함수나 dict 등에서 개괄호 직전에 띄어쓰지 않는다.
```pydocstring
spam(1)
dct['key'] = lst[index]
```
6. assignment 시에 = 의 양쪽을 한 칸 띄운다.
7. 복합 연산의 경우 우선순위에 따라 들여쓰기 여부를 결정한다.
```pydocstring
hypot2 = x*x + y*y
c = (a+b) * (a-b)
```
8. Function Annotation 은 콜론(:) 이후 한 칸 띄어서 작성하고 return Annotation 은 -> 이후 한 칸 띄어서 작성한다.
```pydocstring
def munge(input: AnyStr): ...
def munge() -> PosInt: ...
```
9. 함수의 default argument 는 = 의 양쪽을 띄어쓰지 않는다.
```pydocstring
def complex(real, imag=0.0)
```
10. Function Annotation 이 있는 default argument 의 경우 = 의 양쪽을 한 칸 띄어쓴다.
```pydocstring
def munge(sep: AnyStr = None): ...
```

---

#### Trailing Commas

1. 인자가 1개인 tuple 의 assignment 를 위해 명시적으로 괄호를 작성한다.
```pydocstring
FILES = ('setup.cfg',)
```
2. 인자가 한 개인 tuple 을 제외하고 one-line assignment 의 경우 trailing comma 를 사용하지 않는다.
3. multi-line assignment 의 경우 trailing comma 사용을 허용한다.
```pydocstring
FILES = [
       'setup.cfg',
       'tox.ini',
       ]
```

---

#### Comments

1. identifier 가 아닌 이상 Capitalized 로 완전한 문장을 작성한다.
2. 비영어권 국가의 경우 100% 확신하지 않는 이상 comments 는 영어로 작성한다.
3. \# 이후 한 칸 띄우고 주석을 작성한다.
4. inline comments 는 정말 필요하지 않는 이상 사용하지 않는다.

---

#### Docstrings

1. public modules, functions, classes and methods 의 docstring 을 작성한다.
2. non-public methods 의 docstring 작성 유무는 선택이나 최소 Comments 를 작성하여 무슨 역할을 하는지 알 수 있도록 한다.

---

#### Namings

1. \_single\_leading\_underscore 은 weak internal use 를 가리키는 데에 사용된다. 예를 들어 from M import * 을 할 경우 \_ 로 시작하는 값은 import 되지 않는다.
2. single_trailing_underscore\_ 은 python builtin keyword 와의 충돌을 회피하기 위해 사용한다.
```pydocstring
Tkinter.Toplevel(master, class_='ClassName')
```
3. \_\_double_leading_underscore 는 클래스 내부에서 mangling 된다. FooBar 클래스 내에서 선언된 __boo 는 _FooBar__boo 가 된다.
4. \_\_double_leading_and_trailing_underscore\_\_ 는 \_\_init\_\_, \_\_name\_\_ 등과 같은 magic attribute 이다. 미리 정의된 magic attribute 만 사용하도록 한다.
5. 'l'(lowercase l), 'O'(uppercase O), 'I'(uppercase I) 는 single character 변수로 사용하지 않는다.
6. module name 은 짧아야 하고, 모두 lowercase 여야 한다. _ 는 가독성을 위해 사용 가능하다.
7. 단 파이썬 패키지는 _ 사용을 지양한다.
8. C/C++ extension 과 이를 accompanying 하는 파이썬 패키지가 존재하는 경우 C/C++ extension 은 \_ 로 시작한다. (ex. \_socket)
9. 클래스 이름은 CapitalizedWords 로 작성한다.
10. Type Variable 은 CapitalizedWords 로 작성하고, covariant, contravariant 유무에 따라 suffix 로 \_co, \_contra 를 사용한다.
```pydocstring
from typing import TypeVar
\#
VT_co = TypeVar('VT_co', covariant=True)
KT_contra = TypeVar('KT_contra', contravariant=True)
```
11. Exception 의 경우 CamelCase 로 쓰되 suffix 로 Error 를 붙인다.
12. Function, Methods 및 variable 의 경우 lowercase_with_underscore 를 사용한다.
13. Global Variable 역시 lowercase_with_underscore 를 사용한다.
14. Instance methods 의 첫 번째 인자는 무조건 self 로 받도록 한다.
15. Class methods 의 첫 번째 인자는 무조건 cls 로 받도록 한다.
16. CONSTANTS 는 UPPERCASE_WITH_UNDERSCORE 를 사용한다.

---

### Recommendations

1. public 과 non_public attributes 를 잘 구분해야 한다. 만약 애매하다면 non_public 으로 설정한다.
2. None 과 같은 singletons 는 is 와 is not 으로 비교한다.
3. ordering operation 을 정의할 때는 \_\_eq\_\_, \_\_ne\_\_, \_\_lt\_\_, \_\_le\_\_, \_\_gt\_\_, \_\_ge\_\_ 의 6 개 ordering 을 모두 정의하도록 한다.
4. 편의성을 위해 functools.total_ordering 을 사용할 수 있다.
5. lambda assignment 보다는 def 함수 선언을 사용한다.
6. BaseException 을 상속하기 보다는 Exception 을 상속한다.
7. try ... except 에서 except 구문에 가능한 Error 를 기술한다.
8. Error 를 catch 할 필요가 있을 경우 explicit name 을 지정하도록 한다.
```pydocstring
try:
       process_data()
except Exception as exc:
       raise DataProcessingFailedError(str(exc))
```
9. try clause 에는 최소한의 코드 조각만 들어갈 수 있도록 한다. 이후 처리는 else 또는 finally 에서 수행한다.
```pydocstring
try:
    value = collection[key]
except KeyError:
    return key_not_found(key)
else:
    return handle_value(value)
```
10. context managers 가 자원의 획득 및 방출 외의 다른 작업을 한다면 분리된 함수에 의해서 실행되어야 한다.
```pydocstring
with conn.begin_transaction():
       do_stuff_in_transaction(conn)
```
11. 함수는 명시적으로 return 을 반환해야 한다.
```pydocstring
# Correct:
#
def foo(x):
    if x >= 0:
        return math.sqrt(x)
    else:
        return None
#
# Wrong:
def foo(x):
    if x >= 0:
        return math.sqrt(x)
```
12. string module 보다는 string methods 를 사용한다.
13. 첫 글자 또는 마지막 글자를 체크하기 위해 slicing 보다는 startswith, endswith 를 사용한다.
14. object type 비교를 위해 isinstance 를 사용하고 type(A) is B 의 사용을 지양한다.
15. string, list, tuples, dict 등에서 empty 가 if 구문에서 false 로 인지되는 것을 사용한다.
```pydocstring
# Correct:
if not seq:
if seq:
#
# Wrong:
if len(seq):
if not len(seq):
```
16. bool 을 비교하지 않는다.
```pydocstring
# Correct:
if greeting:
# Wrong:
if greeting == True:
if greeting is True:
```
17. return, break, continue 등 control statement 는 finally 구문 안에서 사용하지 않는다.
