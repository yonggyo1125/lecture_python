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
- 