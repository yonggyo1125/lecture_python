# 함수

## 함수란 무엇인가?

- 입력값을 가지고 어떤 일을 수행한 후 그 결과물을 내어 놓는 것이 바로 함수가 하는 일이다.
- 
## 함수를 사용하는 이유는 무엇일까?
- 반복되는 부분이 있을 경우, ‘반복적으로 사용되는 가치 있는 부분’을 한 뭉치로 묶어 ‘어떤 입력값을 주었을 때 어떤 결괏값을 리턴해 준다’라는 식의 함수로 작성하는 것이다.
- 함수를 사용하는 또 다른 이유는 자신이 작성한 프로그램을 기능 단위의 함수로 분리해 놓으면 프로그램 흐름을 일목요연하게 볼 수 있기 때문이다. 
- 이렇게 되면 프로그램 흐름도 잘 파악할 수 있고 오류가 어디에서 나는지도 쉽게 알아차릴 수 있다.

## 파이썬 함수의 구조

```python
def 함수_이름(매개변수):
    수행할_문장1
    수행할_문장2
    ...
```

- def는 함수를 만들 때 사용하는 예약어이며, 함수 이름은 함수를 만드는 사람이 임의로 만들 수 있다. 
- 함수 이름 뒤 괄호 안의 매개변수는 이 함수에 입력으로 전달되는 값을 받는 변수이다.
- 이렇게 함수를 정의한 후 if, while, for 문 등과 마찬가지로 함수에서 수행할 문장을 입력한다.

```python
def add(a, b): 
    return a + b
```

- 위 함수는 다음과 같이 풀이된다.

```
이 함수의 이름은 add이고 입력으로 2개의 값을 받으며 리턴값(출력값)은 2개의 입력값을 더한 값이다.
```

```python
>>> def add(a, b):
...     return a+b
...
>>>
```

- add 함수를 사용해 보자.

```python
>>> a = 3
>>> b = 4
>>> c = add(a, b)  # add(3, 4)의 리턴값을 c에 대입
>>> print(c)
7
```

## 매개변수와 인수

- 매개변수는 함수에 입력으로 전달된 값을 받는 변수, 인수는 함수를 호출할 때 전달하는 입력값을 의미한다.

```python
def add(a, b):  # a, b는 매개변수
    return a+b

print(add(3, 4))  # 3, 4는 인수
```

## 입력값과 리턴값에 따른 함수의 형태

- 함수는 들어온 입력값을 받은 후 어떤 처리를 하여 적절한 값을 리턴해 준다.
- 함수의 형태는 입력값과 리턴값의 존재 유무에 따라 4가지 유형으로 나뉜다. 자세히 알아보자.

### 일반적인 함수

- 입력값이 있고 리턴값이 있는 함수가 일반적인 함수이다. 

```python
def 함수_이름(매개변수):
    수행할_문장
    ...
    return 리턴값
```

- 일반적인 함수의 예

```python
def add(a, b): 
    result = a + b 
    return result
```

- 이 함수를 사용하는 방법은 다음과 같다. 

```python
>>> a = add(3, 4)
>>> print(a)
7
```

- 이처럼 입력값과 리턴값이 있는 함수의 사용법을 정리하면 다음과 같다.

```python
리턴값을_받을_변수 = 함수_이름(입력_인수1, 입력_인수2, ...)
```

### 입력값이 없는 함수

```python
>>> def say(): 
...     return 'Hi' 
```

```python
>>> a = say()
>>> print(a)
Hi
```

-  say()처럼 괄호 안에 아무런 값도 넣지 않아야 한다. 이 함수는 입력값은 없지만, 리턴값으로 "Hi"라는 문자열을 리턴한다. 즉, a = say()처럼 작성하면 a에 "Hi"라는 문자열이 대입되는 것이다.
- 입력값이 없고 리턴값만 있는 함수는 다음과 같이 사용한다.

```python
리턴값을_받을_변수 = 함수_이름()
```

### 리턴값이 없는 함수

```python
>>> def add(a, b): 
...     print("%d, %d의 합은 %d입니다." % (a, b, a+b))
```

```python
>>> add(3, 4)
3, 4의 합은 7입니다.
```

- 리턴값이 없는 함수는 다음과 같이 사용한다.

```python
함수_이름(입력_인수1, 입력_인수2, ...)
```
- print 문은 함수의 구성 요소 중 하나인 ‘수행할_문장’에 해당하는 부분일 뿐이다. 리턴값은 당연히 없다. 리턴값은 오직 return 명령어로만 돌려받을 수 있다.
- 리턴받을 값을 a 변수에 대입하고 a 값을 출력해 보면 리턴값이 있는지, 없는지 알 수 있다.

```python
>>> a = add(3, 4)
3, 4의 합은 7입니다.
>>> print(a)
None
```

- add 함수처럼 리턴값이 없을 때 <code>a = add(3, 4)</code>처럼 쓰면 함수 add는 리턴값으로 a 변수에 None을 리턴한다. 
- None을 리턴한다는 것은 리턴값이 없다는 것이다.

### 입력값도, 리턴값도 없는 함수

```python
>>> def say(): 
...     print('Hi')
```

```python
>>> say()
Hi
```

- 입력값도, 리턴값도 없는 함수는 다음과 같이 사용한다.

```python
함수_이름()
```

## 매개변수를 지정하여 호출하기
- 함수를 호출할 때 매개변수를 지정할 수도 있다.

```python
>>> def sub(a, b):
...     return a - b
```

- 다음과 같이 매개변수를 지정하여 사용할 수 있다.

```python
>>> result = sub(a=7, b=3)  # a에 7, b에 3을 전달
>>> print(result)
4
```

- 매개변수를 지정하면 다음과 같이 순서에 상관없이 사용할 수 있다는 장점이 있다.

```python
>>> result = sub(b=5, a=3)  # b에 5, a에 3을 전달
>>> print(result)
-2
```

## 입력값이 몇 개가 될지 모를 때는 어떻게 해야 할까?

```python
def 함수_이름(*매개변수):
    수행할_문장
    ...
```

- 일반적으로 볼 수 있는 함수 형태에서 괄호 안의 매개변수 부분이 <code>*매개변수</code>로 바뀌었다.

### 여러 개의 입력값을 받는 함수 만들기

- 여러 개의 입력값을 모두 더하는 함수를 직접 만들어 보자.

```python
>>> def add_many(*args): 
...     result = 0 
...     for i in args: 
...         result = result + i   # *args에 입력받은 모든 값을 더한다.
...     return result 
```

- 위에서 만든 add_many 함수는 입력값이 몇 개이든 상관없다. <code>*args</code>처럼 매개변수 이름 앞에 *을 붙이면 입력값을 전부 모아 튜플로 만들어 주기 때문이다.
- 여기에서 <code>*args</code>는 임의로 정한 변수 이름이다. <code>*pey</code>, <code>*python</code>처럼 아무 이름이나 써도 된다.

> args는 인수를 뜻하는 영어 단어 arguments의 약자이며 관례적으로 자주 사용한다.

- 작성한 add_many 함수를 다음과 같이 사용해 보자.

```python
>>> result = add_many(1,2,3)
>>> print(result)
6
>>> result = add_many(1,2,3,4,5,6,7,8,9,10)
>>> print(result)
55
```

- *arg와 다른 매개변수를 함께 사용하는 예

```python
>>> def add_mul(choice, *args): 
...     if choice == "add":   # 매개변수 choice에 "add"를 입력받았을 때
...         result = 0 
...         for i in args: 
...             result = result + i 
...     elif choice == "mul":   # 매개변수 choice에 "mul"을 입력받았을 때
...         result = 1 
...         for i in args: 
...             result = result * i 
...     return result
```

- 여러 개의 입력값을 의미하는 <code>*args</code> 매개변수 앞에 choice 매개변수가 추가되어 있다.
- 이 함수는 다음과 같이 사용할 수 있다.

```python
>>> result = add_mul('add', 1,2,3,4,5)
>>> print(result)
15
>>> result = add_mul('mul', 1,2,3,4,5)
>>> print(result)
120
```

### 키워드 매개변수, kwargs

- 키워드 매개변수를 사용할 때는 매개변수 앞에 별 2개(<code>**</code>)를 붙인다. 

```python
>>> def print_kwargs(**kwargs):
...     print(kwargs)
```

- print_kwargs는 입력받은 매개변수 kwargs를 출력하는 단순한 함수이다.

```python
>>> print_kwargs(a=1)
{'a': 1}
>>> print_kwargs(name='foo', age=3)
{'age': 3, 'name': 'foo'}
```

- <code>\**kwargs</code>처럼 매개변수 이름 앞에 <code>\**</code>을 붙이면 매개변수 kwargs는 딕셔너리가 되고 모든 <code>Key=Value</code> 형태의 입력값이 그 딕셔너리에 저장된다는 것을 알 수 있다.

## 함수의 리턴값은 언제나 하나이다

```python
>>> def add_and_mul(a,b): 
...     return a+b, a*b
```

- 이 함수를 다음과 같이 호출하면 어떻게 될까?

```python
>>> result = add_and_mul(3,4)
```

- add_and_mul 함수의 리턴값 <code>a+b</code>와 <code>a\*b</code>는 튜플값 하나인 (a+b, a*b)로 리턴된다.
- 따라서 result 변수는 다음과 같은 값을 가지게 된다

```python
result = (7, 12)
```

- 이 하나의 튜플 값을 2개의 값으로 분리하여 받고 싶다면 함수를 다음과 같이 호출하면 된다.

```python
>>> result1, result2 = add_and_mul(3, 4)
```

- 이렇게 호출하면 <code>result1, result2 = (7, 12)</code>가 되어 result1은 7, result2는 12가 된다.

- 또 다음과 같은 의문이 생길 수도 있다.

```python
>>> def add_and_mul(a,b): 
...     return a+b 
...     return a*b
```

```python
>>> result = add_and_mul(2, 3)
>>> print(result)
5
```

- <code>add_and_mul(2, 3)</code>의 리턴값은 5 하나뿐이다. 두 번째 return 문인 <code>return a * b</code>는 실행되지 않았다는 뜻이다. 
- 즉, 함수는 return 문을 만나는 순간, 리턴값을 돌려 준 다음 함수를 빠져나가게 된다.
- 따라서 이 함수는 다음과 완전히 동일하다.

```python
>>> def add_and_mul(a,b): 
...     return a+b 
```

- 즉 함수는 return문을 만나는 순간 결괏값을 돌려준 다음 함수를 빠져나가게 된다.

### return의 또 다른 쓰임새

- 특별한 상황일 때 함수를 빠져나가고 싶다면 return을 단독으로 써서 함수를 즉시 빠져나갈 수 있다. 다음 예를 살펴보자.

```python
>>> def say_nick(nick): 
...     if nick == "바보": 
...         return 
...     print("나의 별명은 %s 입니다." % nick)
```

- 만약 입력값으로 '바보'라는 값이 들어오면 문자열을 출력하지 않고 함수를 즉시 빠져나간다.

```python
>>> say_nick('야호')
나의 별명은 야호입니다.
>>> say_nick('바보')
>>>
```

## 매개변수에 초깃값 미리 설정하기

```python
# default1.py
def say_myself(name, age, man=True): 
    print("나의 이름은 %s 입니다." % name) 
    print("나이는 %d살입니다." % age) 
    if man: 
        print("남자입니다.")
    else: 
        print("여자입니다.")
```

- 위 함수를 보면 매개변수가 <code>name, age, man=True</code>이다.
- <code>man=True</code>처럼 매개변수에 미리 값을 넣어 준 것이다. 이것이 바로 함수의 매개변수에 초깃값을 설정하는 방법이다.
- say_myself 함수는 다음처럼 2가지 방법으로 사용할 수 있다.

```python
say_myself("이이름", 27)
```

```python
say_myself("이이름", 27, True)
```

- man이라는 변수에는 입력값을 주지 않았지만, man은 초깃값 True를 갖게 된다.
- say_myself 함수를 사용한 2가지 방법은 모두 다음처럼 동일한 결과를 출력

```
나의 이름은 이이름입니다.
나이는 27살입니다.
남자입니다.
```

- 초깃값이 설정된 부분을 False로 바꿔 호출해 보자.

```python
say_myself("이이름", 27, False)
```

```
나의 이름은 이이름입니다.
나이는 27살입니다.
여자입니다.
```

### 유의점 
- 매개변수로 <code>(name, age, man=True)</code>는 되지만, <code>(name, man=True, age)</code>는 안 된다는 것
- 즉, 초기화하고 싶은 매개변수는 항상 뒤쪽에 놓아야 한다.

## 함수 안에서 선언한 변수의 효력 범위

```python
# vartest.py
a = 1
def vartest(a):
    a = a +1

vartest(a)
print(a)
```

- 먼저 a라는 변수를 생성하고 1을 대입했다. 그리고 입력으로 들어온 값에 1을 더해 주고 결괏값은 리턴하지 않는 vartest 함수를 선언했다. 그리고 vartest 함수에 입력값으로 a를 주었다. 마지막으로 a의 값을 print(a)로 출력했다.
- vartest 함수에서 매개변수 a의 값에 1을 더했으므로 2가 출력될 것 같지만, 프로그램 소스를 작성해서 실행해 보면 결괏값은 1이 나온다. 
- 그 이유는 함수 안에서 사용하는 매개변수는 함수 안에서만 사용하는 ‘함수만의 변수’이기 때문이다.
- 즉, <code>def vartest(a)</code>에서 입력값을 전달받는 매개변수 a는 함수 안에서만 사용하는 변수일 뿐, 함수 밖의 변수 a와는 전혀 상관없다는 뜻이다.
- 따라서 vartest 함수는 다음처럼 매개변수 이름을 hello로 바꾸어도 이전의 vartest 함수와 완전히 동일하게 동작한다.

```python
def vartest(hello):
    hello = hello + 1
```

- 즉, 함수 안에서 사용하는 매개변수는 함수 밖의 변수 이름과는 전혀 상관없다는 뜻이다.

```python
# vartest_error.py
def vartest(a):
    a = a + 1

vartest(3)
print(a)
```

- vartest(3)을 수행하면 vartest 함수 안에서 a는 4가 되지만, 함수를 호출하고 난 후 print(a) 문장은 오류가 발생하게 된다.
- 그 이유는 print(a)에서 사용한 a 변수는 어디에도 선언되지 않았기 때문이다. 
- 즉, 함수 안에서 선언한 매개변수는 함수 안에서만 사용될 뿐, 함수 밖에서는 사용되지 않는다. 

## 함수 안에서 함수 밖의 변수를 변경하는 방법

### return 사용하기

```python
# vartest_return.py
a = 1 
def vartest(a): 
    a = a +1 
    return a

a = vartest(a) 
print(a)
```

- artest 함수는 입력으로 들어온 값에 1을 더한 값을 리턴하도록 변경했다. 따라서 <code>a = vartest(a)</code>라고 작성하면 a에는 vartest 함수의 리턴값이 대입된다.
- vartest 함수 안의 a 매개변수는 함수 밖의 a와는 다른 것이다.

### global 명령어 사용하기

```python
# vartest_global.py
a = 1 
def vartest(): 
    global a 
    a = a+1

vartest() 
print(a)
```

- global a 문장은 함수 안에서 함수 밖의 a 변수를 직접 사용하겠다는 뜻
- 하지만 프로그래밍을 할 때 global 명령어는 사용하지 않는 것이 좋다. 함수는 독립적으로 존재하는 것이 좋기 때문이다.
- 외부 변수에 종속적인 함수는 그다지 좋은 함수가 아니다. 따라서 되도록 global 명령어를 사용하는 이 방법은 피하고 첫 번째 방법을 사용하기를 권한다.

## lambda 예약어

- lambda는 함수를 생성할 때 사용하는 예약어로, def와 동일한 역할을 한다. 
- 보통 함수를 한 줄로 간결하게 만들 때 사용한다. 
- def를 사용해야 할 정도로 복잡하지 않거나 def를 사용할 수 없는 곳에 주로 쓰인다.

### 사용법

```
함수_이름 = lambda 매개변수1, 매개변수2, ... : 매개변수를_이용한_표현식
```

### 사용예

```python
>>> add = lambda a, b: a + b
>>> result = add(3, 4)
>>> print(result)
7
```

> lambda로 만든 함수는 return 명령어가 없어도 표현식의 결괏값을 리턴한다.