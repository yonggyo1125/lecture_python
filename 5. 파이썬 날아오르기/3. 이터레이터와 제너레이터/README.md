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
