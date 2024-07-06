# 예외 처리

## 오류는 언제 발생하는가?

- 오류를 처리하는 방법을 공부하기 전에 어떤 상황에서 오류가 발생하는지 한번 알아보자. 오타를 입력했을 때 발생하는 구문 오류 같은 것이 아닌 실제 프로그램에서 자주 발생하는 오류를 중심으로 살펴보자.
- 먼저 존재하지 않는 파일을 사용하려고 시도했을 때 발생하는 오류이다.

```python
>>> f = open("나없는파일", 'r')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
FileNotFoundError: [Errno 2] No such file or directory: '나없는파일'
```

- 위 예에서 볼 수 있듯이 없는 파일을 열려고 시도하면 FileNotFoundError 오류가 발생한다.
- 이번에는 0으로 다른 숫자를 나누는 경우를 생각해 보자. 이 역시 자주 발생하는 오류이다.

```python
>>> 4 / 0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
```

- 4를 0으로 나누려고 하니 ZeroDivisionError 오류가 발생한다.
- 1가지 예를 더 들어 보자. 다음 오류는 정말 빈번하게 일어난다.

```python
>>> a = [1, 2, 3]
>>> a[3]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

- a\[3\]은 a의 네 번째 요솟값을 가리키는데, a 리스트에는 값이 3개밖에 없으므로(\[1, 2, 3\]) 값을 얻을 수 없다. 따라서 IndexError 오류가 발생한다. 파이썬은 이런 오류가 발생하면 프로그램을 중단하고 오류 메시지를 보여 준다.

## 오류 예외 처리 기법

### try-except 문

- 다음은 오류를 처리하기 위한 try-except 문의 기본 구조이다.

```python
try:
    ...
except [발생오류 [as 오류변수]]:
    ...
```

- try 블록 수행 중 오류가 발생하면 except 블록이 수행된다. 하지만 try 블록에서 오류가 발생하지 않는다면 except 블록은 수행되지 않는다.
- except 구문을 자세히 살펴보자.

```python
except [발생오류 [as 오류변수]]:
```

- 위 구문을 보면 []를 사용하는데, 이 기호는 괄호 안의 내용을 생략할 수 있다는 관례적인 표기법이다. 즉, except 구문은 다음 3가지 방법으로 사용할 수 있다.

### try-except만 쓰는 방법

```python
try:
    ...
except:
    ...
```

- 이 경우에는 오류의 종류에 상관없이 오류가 발생하면 except 블록을 수행한다.

### 발생 오류만 포함한 except 문

```python
try:
    ...
except 발생오류:
    ...
```

- 이 경우는 오류가 발생했을 때 except 문에 미리 정해 놓은 오류와 동일한 오류일 경우에만 except 블록을 수행한다는 뜻이다.

### 발생 오류와 오류 변수까지 포함한 except 문

```python
try:
    ...
except 발생오류 as 오류변수:
    ...
```

- 이 경우는 두 번째 경우에서 오류의 내용까지 알고 싶을 때 사용하는 방법이다.

```python
# try_except.py
try:
    4 / 0
except ZeroDivisionError as e:
    print(e)
```

- 위처럼 4를 0으로 나누려고 하면 ZeroDivisionError가 발생하여 except 블록이 실행되고 오류 변수 e에 담기는 오류 메시지를 출력할 수 있다. 출력되는 오류 메시지는 다음과 같다.

```
division by zero
```

### try-finally 문

- finally 절은 try 문 수행 도중 예외 발생 여부에 상관없이 항상 수행된다. 
- 보통 finally 절은 사용한 리소스를 close해야 할 때 많이 사용한다.

```python
# try_finally.py
try:
    f = open('foo.txt', 'w')
    # 무언가를 수행한다.

    (... 생략 ...)

finally:
    f.close()  # 중간에 오류가 발생하더라도 무조건 실행된다.
```

- foo.txt 파일을 쓰기 모드로 연 후 예외 발생 여부에 상관없이 항상 파일을 닫아 주려면 try-finally 문을 사용하면 된다.

### 여러 개의 오류 처리하기

```python
try:
    ...
except 발생오류1:
   ... 
except 발생오류2:
   ...
```

- 즉, 0으로 나누는 오류와 인덱싱 오류를 다음과 같이 처리할 수 있다.

```python
# many_error.py
try:
    a = [1,2]
    print(a[3])
    4/0
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
except IndexError:
    print("인덱싱 할 수 없습니다.")
```

- a는 2개의 요솟값을 가지고 있으므로 a\[3\]이 IndexError를 발생시켜 "인덱싱할 수 없습니다."라는 문자열을 출력할 것이다. 인덱싱 오류가 먼저 발생했으므로 <code>4 / 0</code>에 따른 ZeroDivisionError 오류는 발생하지 않는다.
- 앞에서 알아본 것과 마찬가지로 오류 메시지도 다음과 같이 확인할 수 있다.

```python
try:
    a = [1,2]
    print(a[3])
    4/0
except ZeroDivisionError as e:
    print(e)
except IndexError as e:
    print(e)
```

- 프로그램을 실행하면 ‘list index out of range’라는 오류 메시지가 출력될 것이다.
- 다음과 같이 ZerroDivisionError와 IndexError를 함께 처리할 수도 있다.

```python
try:
    a = [1,2]
    print(a[3])
    4/0
except (ZeroDivisionError, IndexError) as e:
    print(e)
```

### try-else 문

```python
try:
    ...
except [발생오류 [as 오류변수]]:
    ...
else:  # 오류가 없을 경우에만 수행
    ...
```

- try 문 수행 중 오류가 발생하면 except 절, 오류가 발생하지 않으면 else 절이 수행된다.

```python
# try_else.py
try:
    age=int(input('나이를 입력하세요: '))
except:
    print('입력이 정확하지 않습니다.')
else:
    if age <= 18:
        print('미성년자는 출입금지입니다.')
    else:
        print('환영합니다.')
```

- 만약 '나이를 입력하세요: '라는 질문에 숫자가 아닌 다른 값을 입력하면 오류가 발생하여 '입력이 정확하지 않습니다.'라는 문장을 출력한다. 오류가 없을 경우에만 else 절이 수행된다.

### 오류 회피하기

- 코드를 작성하다 보면 특정 오류가 발생할 경우 그냥 통과시켜야 할 때가 있다. 

```python
# error_pass.py
try:
    f = open("나없는파일", 'r')
except FileNotFoundError:
    pass
```

- try 문 안에서 FileNotFoundError가 발생할 경우, pass를 사용하여 오류를 그냥 회피하도록 작성한 예제


## 오류 일부러 발생시키기

- 파이썬은 raise 명령어를 사용해 오류를 강제로 발생시킬 수 있다.
- 예를 들어 Bird 클래스를 상속받는 자식 클래스는 반드시 fly라는 함수를 구현하도록 만들고 싶은 경우(강제로 그렇게 하고 싶은 경우)가 있을 수 있다. 다음 예를 살펴보자.

```python
# error_raise.py
class Bird:
    def fly(self):
        raise NotImplementedError
```

- Bird 클래스를 상속받는 자식 클래스는 반드시 fly 함수를 구현해야 한다는 의지를 보여 준다. 

> NotImplementedError는 파이썬에 이미 정의되어 있는 오류로, 꼭 작성해야 하는 부분이 구현되지 않았을 경우 일부러 오류를 발생시키기 위해 사용한다.


```python
class Eagle(Bird):
    pass

eagle = Eagle()
eagle.fly()
```

- Eagle 클래스는 Bird 클래스를 상속받았다. 그런데 Eagle 클래스는 fly 메서드를 오버라이딩하여 구현하지 않았다. 
- 따라서 eagle 객체의 fly 메서드를 수행하는 순간 Bird 클래스의 fly 메서드가 수행되어 NotImplementedError가 발생한다.

```python
Traceback (most recent call last):
  File "...", line 33, in <module>
    eagle.fly()
  File "...", line 26, in fly
    raise NotImplementedError
NotImplementedError
```

> 상속받는 클래스에서 메서드를 재구현하는 것을 ‘메서드 오버라이딩’이라고 한다.

```python
class Eagle(Bird):
    def fly(self):
        print("very fast")

eagle = Eagle()
eagle.fly()
```

- 위 예처럼 fly 함수를 구현한 후 프로그램을 실행하면 오류 없이 다음 문장이 출력된다.

```python
very fast
```

## 예외 만들기

- 프로그램을 수행하다가 특수한 경우에만 예외 처리를 하려고 종종 예외를 만들어서 사용한다. 
- 예외는 다음과 같이 파이썬 내장 클래스인 Exception 클래스를 상속하여 만들 수 있다.

```python
# error_make.py
class MyError(Exception):
    pass
```

- 별명을 출력하는 함수를 다음과 같이 작성해 보자.

```python
def say_nick(nick):
    if nick == '바보':
        raise MyError()
    print(nick)
```

- 그리고 다음과 같이 say_nick 함수를 호출해 보자.

```python
say_nick("천사")
say_nick("바보")
```

- 저장한 후 프로그램을 실행해 보면 다음과 같이 "천사"가 한 번 출력된 후 MyError가 발생한다.

```python
천사
Traceback (most recent call last):
  File "...", line 11, in <module>
    say_nick("바보")
  File "...", line 7, in say_nick
    raise MyError()
__main__.MyError
```

- 이번에는 예외 처리 기법을 사용하여 MyError 발생을 예외 처리해 보자.

```python
try:
    say_nick("천사")
    say_nick("바보")
except MyError:
    print("허용되지 않는 별명입니다.")
```

- 프로그램을 실행하면 다음과 같이 출력된다.

```python
천사
허용되지 않는 별명입니다.
```

- 만약 오류 메시지를 사용하고 싶다면 다음처럼 예외 처리를 하면 된다.

```python
try:
    say_nick("천사")
    say_nick("바보")
except MyError as e:
    print(e)
```

- 하지만 프로그램을 실행해 보면 print(e)로 오류 메시지가 출력되지 않는 것을 확인할 수 있다. 
- 오류 메시지를 출력했을 때 오류 메시지가 보이게 하려면 오류 클래스에 다음과 같은 <code>\_\_str\_\_</code> 메서드를 구현해야 한다. 
- <code>\_\_str\_\_</code> 메서드는 print(e)처럼 오류 메시지를 print 문으로 출력할 경우에 호출되는 메서드이다.

```python
class MyError(Exception):
    def __str__(self):
        return "허용되지 않는 별명입니다."
```

- 프로그램을 다시 실행해 보면 "허용되지 않는 별명입니다."라는 오류 메시지가 출력되는 것을 확인할 수 있을 것이다.