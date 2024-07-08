# 파이썬 타입 어노테이션

- 파이썬 3.5 버전부터 변수와 함수에 타입을 지정할 수 있는 타입 어노테이션 기능이 추가되었다.

## 동적 언어와 정적 언어

- a 변수에 숫자 1을 대입하고 type 함수를 실행해 보자.

```python
>>> a = 1
>>> type(a)
<class 'int'>
```

- a 변수의 타입은 int형이라는 것을 알 수 있다. 그리고 다시 a 변수에 문자열 "1"을 대입하고 type 함수를 실행해 보자.

```python
>>> a = "1"
>>> type(a)
<class 'str'>
```

- a 변수의 타입이 str형으로 바뀌었다. 이렇게 프로그램 실행 중에 변수의 타입을 동적으로 바꿀 수 있으므로 파이썬을 동적 프로그래밍 언어(dynamic programming language)라고 한다.
- 파이썬과 달리 자바는 정수형(int) 변수 a에 숫자 1을 대입하고 다시 문자열 "1"을 대입하려 할 때 컴파일 오류가 발생한다.

```java 
int a = 1;  // a 변수를 int형으로 지정
a = "1";  // a 변수에 문자열을 대입할 수 없으므로 컴파일 에러
```

- 자바는 한 번 변수에 타입을 지정하면 지정한 타입 외에 다른 타입은 사용할 수 없으므로 정적 프로그래밍 언어(static programming language)라고 한다.

### 동적 언어의 장단점

- 파이썬과 같은 동적 언어는 타입에 자유로워 유연한 코딩이 가능하므로 쉽고 빠르게 프로그램을 만들 수 있다. 그리고 타입 체크를 위한 코드가 없으므로 비교적 깔끔한 소스 코드를 생성할 수 있다. 하지만 프로젝트의 규모가 커질수록 타입을 잘못 사용해 버그가 생길 확률도 높아진다.

> 안전성을 선호하는 금융권 프로젝트에서는 이런 이유로 동적 언어보다는 정적 언어를 주요 언어로 선택하는 경향이 많다.

## 파이썬 타입 어노테이션

- 파이썬은 동적 언어의 단점을 극복하기 위해 3.5 버전부터 타입 어노테이션 기능을 지원하기 시작했다. 
- 다만 정적 언어에서와 같은 적극적인 타입 체크가 아니라 타입 어노테이션(type annotation), 즉 타입에 대한 힌트를 알려 주는 정도의 기능만 지원한다.
- 타입 어노테이션은 다음과 같이 사용한다.

```python
num: int = 1
```

- 변수 이름 바로 뒤에 <code>: int</code>와 같이 사용해 num 변수가 int형이라는 것을 명시한다.

```python
def add(a: int, b: int) -> int:
    return a + b
```

- 함수의 매개변수에도 같은 규칙을 적용하여 매개변수의 타입을 명시할 수 있다. 그리고 <code>-> int</code>처럼 사용해 함수의 리턴값도 타입을 명시할 수 있다.

> 어노테이션 타입으로 정수는 int, 문자열은 str, 리스트는 list, 튜플은 tuple, 딕셔너리는 dict, 집합은 set, 불은 bool을 사용한다.


## mypy

- 파이썬은 타입 어노테이션으로 매개변수의 타입을 명시하더라도 다음과 같이 다른 타입의 인수를 입력할 수 있다.

```python
# c:/doit/typing_sample.py
def add(a: int, b: int) -> int:
    return a + b

result = add(3, 3.4)
print(result)  # 6.4 출력
```

- add 함수의 b 매개변수는 int형이지만, 3.4와 같은 float형 데이터를 사용해도 이 코드는 문제 없이 돌아간다. 파이썬 타입 어노테이션은 체크가 아닌 힌트이기 때문이다.
- 더 적극적으로 파이썬 어노테이션을 활용하려면 mypy를 사용하는 것이 좋다. mypy는 파이썬 표준 라이브러리가 아니므로 다음과 같이 설치한 후에 사용할 수 있다.

```
pip install mypy
```

- mypy 설치 후 다음과 같이 사용해 보자.

```
C:\doit>mypy typing_sample.py
typing_sample.py:5: error: Argument 2 to "add" has incompatible type "float"; expected "int"
Found 1 error in 1 file (checked 1 source file)
```

- mypy로 typing_sample.py 파일을 확인하면 타입이 맞지 않는다는 오류가 발생한다. 다음과 같이 코드를 수정해 보자.

```python
def add(a: int, b: int) -> int:
    return a + b

result = add(3, 4)
print(result)
```

- 오류가 발생했던 3.4를 int형에 맞게 4로 변경했다. 그리고 mypy를 다시 실행해 보면 오류가 없다는 것을 알려 준다

```
c:\doit>mypy typing_sample.py
Success: no issues found in 1 source file
```
