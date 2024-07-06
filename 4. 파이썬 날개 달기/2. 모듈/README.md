# 모듈
- 모듈이란 함수나 변수 또는 클래스를 모아 놓은 파이썬 파일이다.
- 모듈은 다른 파이썬 프로그램에서 불러와 사용할 수 있도록 만든 파이썬 파일이라고도 할 수 있다.
- 파이썬으로 프로그래밍을 할 때 매우 많은 모듈을 사용한다. 다른 사람들이 이미 만들어 놓은 모듈을 사용할 수도 있고 우리가 직접 만들어 사용할 수도 있다. 

## 모듈 만들기

- 모듈에 대해 자세히 살펴보기 전에 간단한 모듈을 한번 만들어 보자.

```python
# mod1.py
def add(a, b):
    return a + b

def sub(a, b): 
    return a-b
```

- 위와 같이 add와 sub 함수만 있는 파일 mod1.py를 만들고 C:\doit 디렉터리에 저장하자. 이 mod1.py 파일이 바로 모듈이다.
- 파이썬 확장자 .py로 만든 파이썬 파일은 모두 모듈이다.

## 모듈 불러오기

```
C:\Users\pahkey>cd C:\doit
C:\doit>dir
...
2014-09-23 오후 01:53 49 mod1.py
...
C:\doit>python
>>> 
```

```python
>>> import mod1
>>> print(mod1.add(3, 4))
7
>>> print(mod1.sub(4, 2))
2
```

- mod1.py 모듈을 불러오기 위해 <code>import mod1</code>이라고 입력했다. 실수로 <code>import mod1.py</code>라고 입력하지 않도록 주의하자.
- import는 이미 만들어 놓은 파이썬 모듈을 사용할 수 있게 해 주는 명령어이다. mod1. py 파일에 있는 add 함수를 사용하기 위해서는 mod1.add처럼 모듈 이름 뒤에 도트 연산자(.)를 붙이고 함수 이름을 쓰면 된다.
  - import는 현재 디렉터리에 있는 파일이나 파이썬 라이브러리가 저장된 디렉터리에 있는 모듈만 불러올 수 있다.
  - 파이썬 라이브러리는 파이썬을 설치할 때 자동으로 설치되는 파이썬 모듈을 말한다.
- import의 사용 방법은 다음과 같다.

```python
import 모듈_이름
```

- 모듈 이름은 mod1.py에서 .py 확장자를 제거한 mod1만을 가리킨다.
- 때로는 mod1.add, mod1.sub처럼 쓰지 않고 add, sub처럼 모듈 이름 없이 함수 이름만 쓰고 싶은 경우도 있을 것이다. 이럴 때는 다음과 같이 사용하면 된다.

```python
from 모듈_이름 import 모듈_함수
```

- 위와 같이 함수를 직접 import하면 모듈 이름을 붙이지 않고 바로 해당 모듈의 함수를 쓸 수 있다.

```python
>>> from mod1 import add
>>> add(3, 4)
7
```

- 그런데 이렇게 하면 mod1.py 파일의 add 함수 하나만 사용할 수 있다. add 함수와 sub 함수 둘 다 모듈 이름을 붙이지 않고 사용하려면 다음 2가지 방법을 참고

```python
from mod1 import add, sub
```

- 첫 번째 방법은 위와 같이 <code>from 모듈_이름 import 모듈_함수1, 모듈_함수2</code>처럼 사용하는 것이다. 쉼표(,)로 구분하여 필요한 함수를 불러올 수 있다.

```python
from mod1 import *
```

- 두 번째 방법은 * 문자를 사용하는 것이다.
- <code>from mod1 import *</code>은 mod1 모듈의 모든 함수를 불러와 사용하겠다는 뜻이다.
- mod1.py 파일에는 함수가 2개밖에 없으므로 위 2가지 방법은 동일하게 적용된다.

## if __name__ == "__main__":의 의미

- 이번에는 mod1.py 파일을 다음과 같이 수정해 보자.


```python
# mod1.py
def add(a, b): 
    return a+b

def sub(a, b): 
    return a-b

print(add(1, 4))
print(sub(4, 2))
```

- add(1, 4)와 sub(4, 2)의 결과를 출력하는 문장을 추가했다. 그리고 출력한 결괏값을 확인하기 위해 mod1.py 파일을 다음과 같이 실행해 보자.

```
C:\doit>python mod1.py
5
2
```

- 예상한 대로 결괏값이 잘 출력된다. 그런데 이 mod1.py 파일의 add와 sub 함수를 사용하기 위해 mod1 모듈을 import할 때는 조금 이상한 문제가 생긴다.

```python
C:\Users\pahkey> cd C:\doit
C:\doit> python
>>> import mod1
5
2
```

- 엉뚱하게도 import mod1을 수행하는 순간 mod1.py 파일이 실행되어 결괏값을 출력한다.
- 이러한 문제를 방지하려면 mod1.py 파일을 다음처럼 수정해야 한다.

```python
# mod1.py
def add(a, b): 
    return a+b

def sub(a, b): 
    return a-b

if __name__ == "__main__":
    print(add(1, 4))
    print(sub(4, 2))
```

- <code>if __name__ == "__main__"</code>을 사용하면 <code>C:\doit>python mod1.py</code>처럼 직접 이 파일을 실행했을 때는 <code>__name__ == "__main__"</code> 이 참이 되어 if 문 다음 문장이 수행된다. 
- 이와 반대로 대화형 인터프리터나 다른 파일에서 이 모듈을 불러 사용할 때는 <code>__name__ == "__main__"</code>이 거짓이 되어 if 문 다음 문장이 수행되지 않는다.

```python
>>> import mod1
>>>
```