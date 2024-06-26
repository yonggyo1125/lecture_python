# if문

## if 문은 왜 필요할까?

- 프로그래밍에서 조건을 판단하여 해당 조건에 맞는 상황을 수행하는 데 쓰는 것이 바로 if 문이다.

```
‘돈이 있으면 택시를 타고 가고, 돈이 없으면 걸어간다.’
```

- 파이썬에서는 위와 같은 상황을 다음과 같이 표현할 수 있다.

```python
>>> money = True
>>> if money:
...     print("택시를 타고 가라")
... else:
...     print("걸어 가라")
...
택시를 타고 가라
```

- money에 True를 대입했으므로 money는 참이다. 따라서 if 문 다음 문장이 수행되어 '택시를 타고 가라'가 출력된다.


## if 문의 기본 구조

```python
if 조건문:
    수행할_문장1
    수행할_문장2
    ...
else:
    수행할_문장A
    수행할_문장B
    ...
```

- 조건문을 테스트해서 참이면 if 문 바로 다음 문장(if 블록)들을 수행하고 조건문이 거짓이면 else 문 다음 문장(else 블록)들을 수행하게 된다. 따라서 else 문은 if 문 없이 독립적으로 사용할 수 없다.

## 들여쓰기 방법 알아보기

- if 문을 만들 때는 if 조건문: 바로 다음 문장부터 if 문에 속하는 모든 문장에 들여쓰기(indentation)를 해야 한다.
- 다음 예를 보면 조건문이 참일 경우 ‘수행할_문장1’을 들여쓰기했고 ‘수행할_문장2’와 ‘수행할_문장3’도 들여쓰기했다.
- 다른 프로그래밍 언어를 사용해 온 사람들은 파이썬에서 ‘수행할_문장’을 들여쓰기하는 것을 무시하는 경우가 많으므로 더 주의해야 한다.


```python
if 조건문:
    수행할_문장1
    수행할_문장2
    수행할_문장3
```

- 다음처럼 작성하면 오류가 발생한다. ‘수행할_문장2’를 들여쓰기하지 않았기 때문이다.

```python
if 조건문:
    수행할_문장1
수행할_문장2
    수행할_문장3
```

- 다음과 같은 코드는 오류가 발생한다.

```python
money = True
if money:
    print("택시를")
print("타고")
    print("가라")
```

- 다음과 같은 경우에도 오류가 발생한다. ‘수행할_문장3’을 들여쓰기했지만, ‘수행할_문장1’이나 ‘수행할_문장2’와 들여쓰기의 깊이가 다르다.
- 즉, 들여쓰기는 언제나 같은 깊이로 해야 한다.

```python
if 조건문:
    수행할_문장1
    수행할_문장2
        수행할_문장3
```

- 마찬가지로 다음과 같은 코드 역시 오류가 발생한다.

```python
money = True
if money:
    print("택시를")
    print("타고")
        print("가라")
```

- 그렇다면 들여쓰기는 공백 문자(\[Spacebar\])로 하는 것이 좋을까, 탭 문자(\[Tab\])로 하는 것이 좋을까? 이에 대한 논란은 파이썬을 사용하는 사람들 사이에서 아직도 계속되고 있다.
- 공백 문자로 하자는 쪽과 탭 문자로 하자는 쪽 모두가 동의하는 내용은 2가지를 혼용해서 쓰지 말자는 것이다.
- 공백 문자로 할 것이라면 공백으로 통일하고, 탭 문자로 할 것이라면 탭으로 통일하자는 말이다. 탭이나 공백은 프로그램 소스에서 눈으로 보이는 것이 아니기 때문에 혼용해서 쓰면 오류의 원인이 되므로 주의하자.

> 요즘 파이썬 커뮤니티에서는 들여쓰기를 할 때 공백 문자 4개를 사용하는 것을 권장한다. 또한 파이썬 에디터는 대부분 탭 문자로 들여쓰기를 하더라도 탭 문자를 공백 문자 4개로 자동 변환하는 기능을 갖추고 있다.

- 조건문 다음에 콜론(:)을 잊지 말자!

## 조건문이란 무엇인가?

- if 조건문에서 ‘조건문’이란 참과 거짓을 판단하는 문장을 말한다.
- 앞에서 살펴본 택시 예제에서 조건문은 money가 된다.

```python
>>> money = True
>>> if money:
```

- money는 True이기 때문에 조건이 참이 되어 if 문 다음 문장을 수행한다.


### 비교 연산자

- 조건문에 비교 연산자(\<, \>, ==, !=, \>=, \<=)를 쓰는 방법에 대해 알아보자.

| 비교연산자  |설명|
|--------|----|
| x \< y |x가 y보다 작다.|
| x \> y |x가 y보다 크다.|
| x == y |x와 y가 같다.|
|x != y|x와 y가 같지 않다.|
|x \>= y|x가 y보다 크거나 같다.|
|x \<= y|x가 y보다 작거나 같다.|

- 이 연산자를 어떻게 사용하는지 알아보자.

```python
>>> x = 3
>>> y = 2
>>> x > y
True
>>>
```

- x에 3, y에 2를 대입한 후 x \> y라는 조건문을 수행하면 True를 리턴한다. x \> y 조건문이 참이기 때문이다.

```python
>>> x < y
False
```

- 위 조건문은 거짓이기 때문에 False를 리턴한다.

```python
>>> x == y
False
```

- x와 y는 같지 않다. 따라서 위 조건문은 거짓이므로 False를 리턴한다.
- 앞에서 살펴본 택시 예제를 다음처럼 바꾸어 보자.

```
만약 3000원 이상의 돈을 가지고 있으면 택시를 타고 가고, 그렇지 않으면 걸어가라.
```

- 이 상황은 다음처럼 프로그래밍할 수 있다.

```python
>>> money = 2000
>>> if money >= 3000:
...     print("택시를 타고 가라")
... else:
...     print("걸어가라")
...
걸어가라
>>>
```

- money \>= 3000 조건문이 거짓이 되기 때문에 else 문 다음 문장을 수행하게 된다.

### and, or, not

|연산자|설명|
|---|----|
|x or y|x와 y 둘 중 하나만 참이어도 참이다.|
|x and y|x와 y 모두 참이어야 참이다.|
|not x|x가 거짓이면 참이다.|


- 다음 예를 통해 or 연산자의 사용법을 알아보자.

```
돈이 3000원 이상 있거나 카드가 있다면 택시를 타고 가고, 그렇지 않으면 걸어가라.
```

```python
>>> money = 2000
>>> card = True
>>> if money >= 3000 or card:
...     print("택시를 타고 가라")
... else:
...     print("걸어가라")
...
택시를 타고 가라
>>>
```
- money는 2000이지만, card가 True이기 때문에 money \>= 3000 or card 조건문이 참이 된다.
- 따라서 if 문에 속한 ‘택시를 타고 가라’ 문장이 출력된다.

### in, not in

|in|not in|
|---|----|
|x in 리스트|x not in 리스트|
|x in 튜플|x not in 튜플|
|x in 문자열|x not in 문자열|

- 영어 단어 in의 뜻이 ‘~안에’라는 것을 생각해 보면 다음 예가 쉽게 이해될 것이다.

```python
>>> 1 in [1, 2, 3]
True
>>> 1 not in [1, 2, 3]
False
```

- 첫 번째 예는 1은 \[1, 2, 3\] 안에 있으므로 참이 되어 True를 리턴한다.
- 두 번째 예는 1은 \[1, 2, 3\] 안에 있으므로 거짓이 되어 False를 리턴한다.
- 다음은 튜플과 문자열에 in과 not in을 적용한 예이다.

```python
>>> 'a' in ('a', 'b', 'c')
True
>>> 'j' not in 'python'
True
```

- 이번에는 우리가 계속 사용해 온 택시 예제에 in을 적용해 보자.

```
만약 주머니에 돈이 있으면 택시를 타고 가고, 없으면 걸어가라.
```

```python
>>> pocket = ['paper', 'cellphone', 'money']
>>> if 'money' in pocket:
...     print("택시를 타고 가라")
... else:
...     print("걸어가라")
...
택시를 타고 가라
>>>
```

- \['paper', 'cellphone', 'money'\] 리스트 안에 'money'가 있으므로 'money' in pocket은 참이 된다.
- 따라서 if 문에 속한 문장이 수행된다.

### 조건문에서 아무 일도 하지 않게 설정하고 싶다면?

- 이럴 때 사용하는 것이 바로 pass이다

```
주머니에 돈이 있으면 가만히 있고, 주머니에 돈이 없으면 카드를 꺼내라.
```

- 위 예를 pass를 적용해서 구현해 보자.

```python
>>> pocket = ['paper', 'money', 'cellphone']
>>> if 'money' in pocket:
...     pass 
... else:
...     print("카드를 꺼내라")
...
```

- pocket 리스트 안에 money 문자열이 있기 때문에 if 문 다음 문장인 pass가 수행되고 아무런 결괏값도 보여 주지 않는다.

## 다양한 조건을 판단하는 elif

- if와 else만으로는 다양한 조건을 판단하기 어렵다.
- else만을 사용하여 조건식을 만들면 복잡해 진다, 이를 해결하기 위해 파이썬에서는 다중 조건 판단을 가능하게 하는 elif를 사용한다.

```python
>>> pocket = ['paper', 'cellphone']
>>> card = True
>>> if 'money' in pocket:
...      print("택시를 타고가라")
... elif card: 
...      print("택시를 타고가라")
... else:
...      print("걸어가라")
...
택시를 타고가라
```

- 즉, elif는 이전 조건문이 거짓일 때 수행된다. if, elif, else를 모두 사용할 때 기본 구조는 다음과 같다.

```python
if 조건문:
    수행할_문장1 
    수행할_문장2
    ...
elif 조건문:
    수행할_문장1
    수행할_문장2
    ...
elif 조건문:
    수행할_문장1
    수행할_문장2
    ...
...
else:
   수행할_문장1
   수행할_문장2
   ... 
```

### if 문을 한 줄로 작성하기

- 앞의 pass를 사용한 예를 보면 if 문 다음에 수행할 문장이 한 줄이고 else 문 다음에 수행할 문장도 한 줄밖에 되지 않는다.

```python
>>> if 'money' in pocket:
...     pass 
... else:
...     print("카드를 꺼내라")
...
```

- 이렇게 수행할 문장이 한 줄일 때 좀 더 간략하게 코드를 작성하는 방법이 있다.

```python
>>> pocket = ['paper', 'money', 'cellphone']
>>> if 'money' in pocket: pass
... else: print("카드를 꺼내라")
...
```

- if 문 다음에 수행할 문장을 콜론(:) 뒤에 바로 적었다. else 문 역시 마찬가지이다.


## 조건부 표현식

- score가 60 이상일 경우 message에 문자열 "success", 아닐 경우에는 문자열 "failure"를 대입하는 코드이다.

```python
if score >= 60:
    message = "success"
else:
    message = "failure"
```

- 파이썬의 조건부 표현식(conditional expression)을 사용하면 위 코드를 다음과 같이 간단히 표현할 수 있다.

```python
message = "success" if score >= 60 else "failure"
```

- 조건부 표현식은 다음과 같이 정의한다.

```python
변수 = 조건문이_참인_경우의_값 if 조건문 else 조건문이_거짓인_경우의_값
```

- 조건부 표현식은 가독성에 유리하고 한 줄로 작성할 수 있어 활용성이 좋다.