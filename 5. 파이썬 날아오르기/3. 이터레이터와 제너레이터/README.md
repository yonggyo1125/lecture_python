# 이터레이터와 제너레이터

- 다음은 늘 사용하던 리스트의 간단한 사용법이다.

```python
for a in [1, 2, 3]:
    print(a)
```

- 리스트 \[1, 2, 3\]을 for 문으로 차례대로 하나씩 출력하는 예제이다. 이렇게 for 문과 같은 반복 구문에 적용할 수 있는 리스트와 같은 객체를 ‘반복 가능(iterable) 객체’라고 한다.


## 이터레이터란?

- 이터레이터는 next 함수 호출 시 계속 그다음 값을 리턴하는 객체이다. 
- 리스트는 반복 가능(iterable)하다는 것을 이미 알아보았다. 그렇다면 리스트는 이터레이터일까? 다음과 같이 확인해 보자.

```python
>>> a = [1, 2, 3]
>>> next(a)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: 'list' object is not an iterator
```

- a라는 리스트로 next 함수를 호출했더니 리스트는 이터레이터 객체가 아니라는 오류가 발생한다. 즉, 반복 가능하다고 해서 이터레이터는 아니라는 말이다. 하지만 반복 가능하다면 다음과 같이 iter 함수를 이용해 이터레이터로 만들 수 있다.

```python
>>> a = [1, 2, 3]
>>> ia = iter(a)
>>> type(ia)
<class 'list_iterator'>
```

- 이제 리스트를 이터레이터로 변경했으므로 next 함수를 호출해 보자.

```python
>>> next(ia)
1
>>> next(ia)
2
>>> next(ia)
3
>>> next(ia)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
StopIteration
```

- next 함수를 호출할 때마다 이터레이터 객체의 요소를 차례대로 리턴하는 것을 확인할 수 있다. 하지만 더는 리턴할 값이 없다면 StopIteration 예외가 발생한다.
- 이터레이터의 값을 가져오는 가장 일반적인 방법은 다음과 같이 for 문을 이용하는 것이다.

```python
>>> a = [1, 2, 3]
>>> ia = iter(a)
>>> for i in ia:
...     print(i)
...
1
2
3
```

- for 문을 이용하면 자동으로 값을 호출하므로 next 함수를 따로 쓸 필요도 없고 StopIteration 예외에 신경 쓸 필요도 없다.
- 이번에는 다음과 같은 예를 살펴보자.

```python
>>> a = [1, 2, 3]
>>> ia = iter(a)
>>> for i in ia:
...     print(i)
...
1
2
3
>>> for i in ia:
...     print(i)
...
>>>
```

- 이처럼 이터레이터는 for 문을 이용하여 반복하고 난 후에는 다시 반복하더라도 더는 그 값을 가져오지 못한다. 즉, for문이나 next로 그 값을 한 번 읽으면 그 값을 다시는 읽을 수 없다는 특징이 있다.

## 이터레이터 만들기

- iter 함수를 이용하면 리스트를 이터레이터로 만들 수 있었다. 이번에는 iter 함수 대신 클래스로 이터레이터를 만들어 보자.
- 이터레이터는 클래스에 <code>\_\_iter\_\_</code>와 <code>\_\_next\_\_</code>라는 2개의 메서드를 구현하여 만들 수 있다. 다음 예를 살펴보자.

```python
# iterator.py
class MyIterator:
    def __init__(self, data):
        self.data = data
        self.position = 0
    
    def __iter__(self):
        return self

    def __next__(self):
        if self.position >= len(self.data):
            raise StopIteration
        result = self.data[self.position]
        self.position += 1
        return result

if __name__ == "__main__":
    i = MyIterator([1, 2, 3])
    for item in i:
        print(item)
```

- MyIterator 클래스는 이터레이터 객체를 생성하기 위해 <code>\_\_iter\_\_</code> 메서드와 <code>\_\_next\_\_</code> 메서드를 구현했다. <code>\_\_iter\_\_</code> 메서드와 <code>\_\_next\_\_</code> 메서드는 생성자 <code>\_\_init\_\_</code> 메서드와 마찬가지로 클래스에서 특별한 의미를 갖는 메서드이다.
- 클래스에 <code>\_\_iter\_\_</code> 메서드를 구현하면 해당 클래스로 생성한 객체는 반복 가능한 객체가 된다. <code>\_\_iter\_\_</code> 메서드는 반복 가능한 객체를 리턴해야 하며 보통 클래스의 객체를 의미하는 self를 리턴한다. 그리고 클래스에 <code>\_\_iter\_\_</code> 메서드를 구현할 경우 반드시 <code>\_\_next\_\_</code> 함수를 구현해야 한다.
- <code>\_\_next\_\_</code> 메서드는 반복 가능한 객체의 값을 차례대로 반환하는 역할을 한다. <code>\_\_next\_\_</code> 메서드는 for 문을 수행하거나 next 함수 호출 시 수행되므로 MyIterator 객체를 생성할 때 전달한 data를 하나씩 리턴하고 더는 리턴할 값이 없으면 StopIteration 예외를 발생시키도록 구현했다.
- 이 코드를 실행하면 다음과 같은 결과를 확인할 수 있다.

```
1
2
3
```

- 이번에는 입력받은 데이터를 역순으로 출력하는 ReverseIterator 클래스를 만들어 보자(설명은 앞의 MyIterator와 마찬가지이므로 생략한다).

```python
# reviterator.py
class ReverseIterator:
    def __init__(self, data):
        self.data = data
        self.position = len(self.data) - 1
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.position < 0:
            raise StopIteration
        result = self.data[self.position]
        self.position -= 1
        return result

if __name__ == "__main__":
    i = ReverseIterator([1, 2, 3])
    for item in i:
        print(item)
```

- 이를 실행하면 다음과 같이 입력받은 데이터를 역순으로 출력한다.

```
3
2
1
```

## 제너레이터란?

- 제너레이터(generator)는 이터레이터를 생성해 주는 함수이다. 
- 제너레이터로 생성한 객체는 이터레이터와 마찬가지로 next 함수 호출 시 그 값을 차례대로 얻을 수 있다. 
- 이때 제너레이터에서는 차례대로 결과를 반환하고자 return 대신 yield 키워드를 사용한다.
- 가장 간단한 제너레이터의 예를 살펴보자.

```python
>>> def mygen():
...     yield 'a'
...     yield 'b'
...     yield 'c'
...
>>> g = mygen()
```

- mygen 함수는 yield 구문을 포함하므로 제너레이터이다. 제너레이터 객체는 <code>g = mygen()</code>과 같이 제너레이터 함수를 호출하여 만들 수 있다. type 명령어로 확인하면 g 객체는 제너레이터 타입의 객체라는 것을 알 수 있다.

```python
>>> type(g)
<class 'generator'>
```

- 이제 다음과 같이 제너레이터의 값을 차례대로 얻어 보자.

```python
>>> next(g)
'a'
```

- 이처럼 제너레이터 객체 g로 next 함수를 실행하면 mygen 함수의 첫 번째 yield 문에 따라 'a' 값을 리턴한다. 
- 여기서 재미있는 점은 제너레이터는 yield라는 문장을 만나면 그 값을 리턴하되 현재 상태를 그대로 기억한다는 것이다. 
- 이것은 마치 음악을 재생하다가 일시 정지 버튼으로 멈춘 것과 비슷한 모양새이다.
- 다시 next() 함수를 실행해 보자.

```python
>>> next(g)
'b'
```

- 이번에는 두 번째 yield 문에 따라 'b' 값을 리턴한다. 계속해서 next 함수를 호출하면 다음과 같은 결과가 출력될 것이다.

```python
>>> next(g)
'c'
>>> next(g)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

## 제너레이터 표현식

```python
# generator.py
def mygen():
    for i in range(1, 1000):
        result = i * i
        yield result

gen = mygen()

print(next(gen))
print(next(gen))
print(next(gen))
```

- mygen 함수는 1부터 1,000까지 각각의 숫자를 제곱한 값을 순서대로 리턴하는 제너레이터이다. 이 예제를 실행하면 총 3번의 next를 호출하므로 다음과 같은 결과가 나올 것이다.

```
1
4
9
```

- 제너레이터는 def를 이용한 함수로 만들 수 있지만, 다음과 같이 튜플 표현식으로 좀 더 간단하게 만들 수도 있다.

```python
gen = (i * i for i in range(1, 1000))
```

- 이 표현식은 mygen 함수로 만든 제너레이터와 완전히 똑같이 기능한다. 여기서 사용한 표현식은 리스트 컴프리헨션(list comprehension) 구문과 비슷하다. 
- 다만 리스트 대신 튜플을 이용한 점이 다르다. 이와 같은 표현식을 ‘제너레이터 표현식(generator expression)’이라고 부른다.

## 제너레이터와 이터레이터

- 지금까지 살펴본 제너레이터는 이터레이터와 서로 상당히 비슷하다는 것을 알 수 있다. 클래스를 이용해 이터레이터를 작성하면 좀 더 복잡한 행동을 구현할 수 있다.  이와 달리 제너레이터를 이용하면 간단하게 이터레이터를 만들 수 있다. 따라서 이터레이터의 성격에 따라 클래스로 만들 것인지, 제너레이터로 만들 것인지를 선택해야 한다.
- 간단한 경우라면 제너레이터 함수나 제너레이터 표현식을 사용하는 것이 가독성이나 유지 보수 측면에서 유리하다. 다음은 <code>(i * i for i in range(1, 1000))</code> 제너레이터를 이터레이터 클래스로 구현한 예이다.

```python
class MyIterator:
    def __init__(self):
        self.data = 1
    
    def __iter__(self):
        return self

    def __next__(self):
        result = self.data * self.data
        self.data += 1
        if self.data >= 1000:
            raise StopIteration
        return result
```

- 이렇게 간단한 경우라면 이터레이터 클래스보다는 제너레이터 표현식을 사용하는 것이 훨씬 간편하고 이해하기 쉽다.

## 제너레이터 활용하기

```python
# generator2.py
import time

def longtime_job():
    print("job start")
    time.sleep(1)  # 1초 지연
    return "done"

list_job = [longtime_job() for i in range(5)]
print(list_job[0])
```

- longtime_job 함수는 총 실행 시간이 1초이다. 이 예제는 longtime_job 함수를 5번 실행해 리스트에 그 결괏값을 담고 그 첫 번째 결괏값을 호출하는 예제이다. 실행하면 다음과 같은 결과를 출력한다.

```
job start
job start
job start
job start
job start
done
```

- 리스트를 만들 때 이미 5개의 함수를 모두 실행하므로 5초의 시간이 소요되고 이와 같은 결과를 출력한다.
- 이번에는 이 예제에 제너레이터를 적용해 보자. 프로그램을 다음과 같이 수정하자.

```python
# generator2.py
import time

def longtime_job():
    print("job start")
    time.sleep(1)
    return "done"

list_job = (longtime_job() for i in range(5))
print(next(list_job))
```
- <code>\[longtime_job() for i in range(5)\]</code> 코드를 제너레이터 표현식<code>(longtime_job() for i in range(5))</code>으로 바꾸었을 뿐이다. 그런데 실행 시 1초의 시간만 소요되고 출력되는 결과도 전혀 다르다.

```
job start
done
```

- 왜냐하면 제너레이터 표현식으로 인해 longtime_job() 함수가 5회가 아닌 1회만 호출되기 때문이다. 이러한 방식을 느긋한 계산법(lazy evaluation)이라고 부른다. 
- 시간이 오래 걸리는 작업을 한꺼번에 처리하기보다는 필요한 경우에만 호출하여 사용할 때 제너레이터는 매우 유용하다.
