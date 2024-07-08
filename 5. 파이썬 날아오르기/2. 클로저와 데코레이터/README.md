# 클로저와 데코레이터

- 클로저는 간단히 말해 함수 안에 내부 함수(inner function)를 구현하고 그 내부 함수를 리턴하는 함수를 말한다.
- 이때 외부 함수는 자신이 가진 변숫값 등을 내부 함수에 전달할 수 있다. 알쏭달쏭한 설명이지만, 예제를 보면 쉽게 이해할 수 있다.
- 어떤 수에 항상 3을 곱해 리턴하는 함수를 생각해 보자. 아마도 다음과 같은 함수를 만들 수 있을 것이다

```python
def mul3(n):
    return n * 3
```

- mul3() 함수는 입력으로 받은 수 n에 항상 3을 곱하여 리턴한다. 이번에는 항상 5를 곱하여 리턴하는 함수를 생각해 보자.

```python
def mul5(n):
    return n * 5
```

- 이처럼 mul5() 함수를 만들 수 있을 것이다. 하지만 이렇게 필요할 때마다 mul6(), mul7(), mul8(), …과 같은 함수를 만드는 것은 매우 비효율적이다. 이 문제를 효율적으로 해결하려면 다음과 같이 클래스를 사용하면 된다.

```python
# closure.py
class Mul:
    def __init__(self, m):
        self.m = m
    
    def mul(self, n):
        return self.m * n

if __name__ == "__main__":
    mul3 = Mul(3)
    mul5 = Mul(5)

    print(mul3.mul(10))  # 30 출력
    print(mul5.mul(10))  # 50 출력
```

- 클래스를 이용해 특정 값을 미리 설정하고 그다음부터 mul() 메서드를 사용하면 원하는 형태로 호출할 수 있다. <code>\_\_call\_\_</code> 메서드를 이용하여 다음과 같이 개선할 수도 있다.

```python
# closure.py
class Mul:
    def __init__(self, m):
        self.m = m

    def __call__(self, n):
        return self.m * n

if __name__ == "__main__":
    mul3 = Mul(3)
    mul5 = Mul(5)

    print(mul3(10))  # 30 출력
    print(mul5(10))  # 50 출력
```

- mul() 함수의 이름을 <code>\_\_call\_\_</code>로 바꾸었다. <code>\_\_call\_\_</code> 함수는 Mul 클래스로 만든 객체에 인수를 전달하여 바로 호출할 수 있도록 하는 메서드이다. <code>\_\_call\_\_</code> 메서드를 이용하면 이 예제처럼 mul3 객체를 mul3(10)처럼 호출할 수 있다.

```python
# wrapper.py
def mul(m):
    def wrapper(n):
        return m * n
    return wrapper

if __name__ == "__main__":
    mul4 = mul(3)
    mul5 = mul(5)

    print(mul3(10))  # 30 출력
    print(mul5(10))  # 50 출력
```

- 외부 함수 mul 안에 내부 함수 wrapper를 구현했다. 그리고 외부 함수는 내부 함수 wrapper를 리턴한다. 함수가 함수를 리턴하는 것이 생소할 수 있겠지만, 파이썬에서는 가능하다.
- 재미있는 사실은 mul 함수에서 wrapper 함수를 리턴할 때 mul 함수 호출 시 인수로 받은 m 값을 wrapper 함수에 저장하여 리턴한다는 점이다. 이것은 마치 클래스가 특정한 값을 설정해 객체를 만드는 과정과 매우 비슷하다. 이런 mul과 같은 함수를 파이썬에서는 클로저(closure)라고 한다.

## 데코레이터란?

- 다음은 "함수가 실행됩니다."라는 문자열을 출력하는 myfunc 함수이다.

```python
def myfunc():
    print("함수가 실행됩니다.")
```

- 이 함수의 실행 시간을 측정해야 한다면 어떻게 해야 할까? 함수 실행 시간은 함수가 시작하는 순간의 시간과 함수가 종료되는 순간의 시간 차이를 구하면 알 수 있다. 따라서 다음과 같이 코드를 수정하면 함수의 실행 시간을 측정할 수 있다.

```python
import time

def myfunc():
    start = time.time()
    print("함수가 실행됩니다.")
    end = time.time()
    print("함수 수행시간: %f 초" % (end-start))

myfunc()
```

- 하지만 실행 시간을 측정해야 하는 함수가 myfunc 말고도 많다면 이런 코드를 모든 함수에 마찬가지로 적용하는 것은 너무 비효율적이다. 이때 클로저를 이용하면 좀 더 효율적인 방법을 찾을 수 있다.

```python
# decorator.py
import time

def elapsed(original_func): # 기존 함수를 인수로 받는다.
    def wrapper():
        start = time.time()
        result = original_func() # 기존 함수를 수행한다.
        end = time.time()
        print("함수 수행시간: %f 초" % (end - start)) # 기존 함수의 수행시간을 출력한다.
        return result
    return wrapper

def myfunc():
    print("함수가 실행됩니다.")

decorated_myfunc = elapsed(myfunc)
decorated_myfunc()
```

- elapsed 함수로 클로저를 만들었다. 이 함수는 함수를 인수로 받는다. 파이썬은 함수도 객체이므로 함수 자체를 인수로 전달할 수 있다.
- 이제 <code>decorated_myfunc = elapsed(myfunc)</code>로 생성한 decorated_myfunc를 decorated_myfunc()로 실행하면 실제로는 elapsed 함수 내부의 wrapper 함수가 실행되고, 이 함수는 전달받은 myfunc 함수를 실행하면서 실행 시간을 함께 출력한다.
- 클로저를 이용하면 기존 함수에 기능을 덧붙이기가 매우 편리하다. 이렇게 기존 함수를 바꾸지 않고 기능을 추가할 수 있게 만드는 elapsed 함수와 같은 클로저를 데코레이터(decorator)라고 한다.

> 'decorate'는 '꾸미다, 장식하다'라는 뜻이므로 데코레이터를 함수를 꾸미는 함수라고 생각해도 된다.

- 이 코드를 실행하면 다음과 같은 결과가 출력된다.

```
함수가 실행됩니다.
함수 수행시간: 0.000029 초
```

- 파이썬 데코레이터는 다음처럼 @ 문자를 이용해 함수 위에 적용하여 사용할 수도 있다.

```python
# decorator.py
import time

def elapsed(original_func):  # 기존 함수를 인수로 받는다.
    def wrapper():
        start = time.time()
        result = original_func() # 기존 함수를 수행한다.
        end = time.time()
        print("함수 수행시간: %f 초" % (end - start)) # 기존 함수의 수행시간을 출력한다.
        return result  # 기존 함수의 수행 결과를 리턴한다.
    return wrapper

@elapsed
def myfunc():
    print("함수가 실행됩니다.")

# decorated_myfunc = elapsed(myfunc)  # @elapsed 데코레이터로 인해 더이상 필요하지 않다.
# decorated_myfunc()    
    
myfunc()
```

- myfunc 함수 바로 위에 <code>@elapsed(@+함수명)</code>라는 데코레이터를 추가했다. 파이썬은 함수 위에 <code>@+함수명</code>이 있으면 데코레이터 함수로 인식한다. 따라서 이제 myfunc 함수는 ‘elapsed 데코레이터’를 통해 수행될 것이다.
- 프로그램을 실행해 보면 마찬가지 결과가 출력되는 것을 확인할 수 있다.

```
함수가 실행됩니다.
함수 수행시간: 0.000029 초
```

- 이번에는 myfunc 함수를 다음과 같이 변경해 보자.

```python
# decorator2.py

... 생략 ...

@elapsed
def myfunc(msg):
    print("'%s'을 출력합니다." % msg)

myfunc("You need python")  # 출력할 메시지를 myfunc 파라미터로 전달한다.
```

- 문자열을 입력받아 출력하도록 myfunc 함수를 수정했다. 하지만 이렇게 코드를 수정하고 실행하면 다음과 같은 오류가 발생한다.

```
Traceback (most recent call last):
  File ... 생략 ...
    myfunc("You need python")
TypeError: wrapper() takes 0 positional arguments but 1 was given
```

- myfunc 함수는 입력 인수가 필요하지만, elapsed 함수 안의 wrapper 함수는 전달받은 myfunc 함수를 입력 인수 없이 호출해 오류가 발생하는 것이다. 그러므로 데코레이터 함수는 기존 함수의 입력 인수에 상관없이 동작하도록 만들어야 한다. 데코레이터는 기존 함수가 어떤 입력 인수를 취할지 알 수 없기 때문이다. 
- 이렇게 전달받아야 하는 기존 함수의 입력 인수를 알 수 없는 경우에는 <code>*args</code>와 <code>**kwargs</code> 매개변수를 이용하면 된다.
- 다음과 같이 코드를 수정하자.

```python
# decorator2.py
import time

def elapsed(original_func):  # 기존 합수를 인수로 받는다.
    def wrapper(*args, **kwargs):  # *args, **kwargs 매개변수 추가
        start = time.time()
        result = original_func(*args, **kwargs)  # 전달받은 *args, **kwargs를 입력파라미터로 기존함수 수행
        end = time.time()
        print("함수 수행시간: %f 초" % (end - start))  # 수행시간을 출력한다.
        return result  # 함수의 결과를 리턴한다.
    return wrapper

@elapsed
def myfunc(msg):
    """ 데코레이터 확인 함수 """
    print("'%s'을 출력합니다." % msg)

myfunc("You need python")
```

- wrapper() 함수의 매개변수로 <code>*args</code>와 <code>**kwargs</code>를 추가하고 기존 함수 실행 시 <code>*args</code>와 <code>**kwargs</code>를 인수로 전달하여 호출하게 했다. 이제 프로그램을 실행하면 오류 없이 다음과 같은 결과를 출력한다.

```
'You need python'을 출력합니다.
함수 수행시간: 0.000027 초
```

### *args와 \*\*kwargs

- <code>*args</code>는 모든 입력 인수를 튜플로 변환하는 매개변수, <code>**kwargs</code>는 모든 ‘키=값’ 형태의 입력 인수를 딕셔너리로 변환하는 매개변수이다. 다음과 같은 형태의 호출을 살펴보자.

```python
>>> func(1, 2, 3, name='foo', age=3)
```

- func 함수가 입력 인수의 개수와 형태에 상관없이 모든 입력을 처리하려면 어떻게 해야 할까?

```python
>>> def func(*arg, **kwargs):
    ...     print(args)
...     print(kwargs)
... 
>>> func(1, 2, 3, name='foo', age=3)
(1, 2, 3)
{'age': 3, 'name': 'foo'}
```

- 이처럼 func 함수에 <code>*args</code>, <code>**kwargs</code>라는 매개변수를 지정하면 다양한 입력 인수를 모두 처리할 수 있다. 
- 이렇게 하면 1, 2, 3 같은 일반 입력은 args 튜플, <code>name = 'foo'</code>와 같은 ‘키=값’ 형태의 입력은 kwargs 딕셔너리로 저장한다.