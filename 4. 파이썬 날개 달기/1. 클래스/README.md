# 클래스

-  파이썬으로 잘 만든 프로그램을 살펴봐도 클래스를 사용하지 않고 작성한 것이 매우 많다. 즉, 클래스는 지금까지 공부한 함수나 자료형처럼 프로그램 작성을 위해 꼭 필요한 요소는 아니다.
- 하지만 프로그램을 작성할 때 클래스를 적재적소에 사용하면 프로그래머가 얻을 수 있는 이익은 많다.

## 계산기 프로그램을 만들며 클래스 알아보기

```python
# calculator.py
result = 0

def add(num):
    global result
    result += num  # 결괏값(result)에 입력값(num) 더하기
    return result  # 결괏값 리턴

print(add(3))
print(add(4))
```

- 입력값을 이전에 계산한 결괏값에 더한 후 리턴하는 add 함수를 위와 같이 작성했다. 이전에 계산한 결괏값을 유지하기 위해서 result 전역 변수(global)를 사용했다.
- 프로그램을 실행하면 예상한 대로 다음과 같은 결괏값이 출력된다.

```python
3 
7
```

- 그런데 만일 한 프로그램에서 2대의 계산기가 필요한 상황이 발생하면?
- 각 계산기는 각각의 결괏값을 유지해야 하므로 위와 같이 add 함수 하나만으로는 결괏값을 따로 유지할 수 없다.
- 이런 상황을 해결하려면 다음과 같이 함수를 각각 따로 만들어야 한다.

```python
# calculator2.py
result1 = 0
result2 = 0

def add1(num):  # 계산기1
    global result1
    result1 += num
    return result1

def add2(num):  # 계산기2
    global result2
    result2 += num
    return result2

print(add1(3))
print(add1(4))
print(add2(3))
print(add2(7))
```

- 똑같은 일을 하는 add1과 add2 함수를 만들고 각 함수에서 계산한 결괏값을 유지하면서 저장하는 전역 변수 result1과 result2를 정의했다.
- 결괏값은 다음과 같이 의도한 대로 출력된다.

```python
3
7
3
10
```

- 계산기 1의 결괏값이 계산기 2에 아무런 영향을 끼치지 않는다는 것을 확인할 수 있다.
- 하지만 계산기가 3개, 5개, 10개로 점점 더 많이 필요해진다면?
- 위와 같은 경우에 클래스를 사용하면 다음과 같이 간단하게 해결할 수 있다.

```python
# calculator3.py
class Calculator:
    def __init__(self):
        self.result = 0
    
    def add(self, num):
        self.result += num
        return self.result

cal1 = Calculator()
cal2 = Calculator()

print(cal1.add(3))
print(cal1.add(4))
print(cal2.add(3))
print(cal2.add(7))
```

- 프로그램을 실행하면 함수 2개를 사용했을 때와 동일한 결과가 출력된다.

```
3
7
3
10
```

- Calculator 클래스로 만든 별개의 계산기 cal1, cal2(파이썬에서는 이것을 ‘객체’라고 부른다)가 각각의 역할을 수행한다. 
- 계산기의 결괏값 역시 다른 계산기의 결괏값과 상관없이 독립적인 값을 유지한다.
- 이렇게 클래스를 사용하면 계산기 대수가 늘어나도 객체를 생성하면 되므로 함수만 사용할 때보다 간단하게 프로그램을 작성할 수 있다. 
- 빼기 기능을 더하고 싶다면 Calculator 클래스에 다음과 같이 빼기 기능을 가진 함수를 추가하면 된다.

```python
class Calculator:
    def __init__(self):
        self.result = 0
    
    def add(self, num):
        self.result += num
        return self.result
        
    def sub(self, num):
        self.result -= num
        return self.result
```

## 클래스와 객체

- 과자 틀 = 클래스 
- 과자 틀로 찍어 낸 과자 = 객체
- 클래스(class)란 똑같은 무언가를 계속 만들어 낼 수 있는 설계 도면(과자 틀)
- 객체(object)란 클래스로 만든 피조물(과자 틀로 찍어 낸 과자)을 뜻한다.
- 클래스로 만든 객체에는 중요한 특징이 있다. 바로 객체마다 고유한 성격을 가진다는 것이다. 과자 틀로 만든 과자에 구멍을 뚫거나 조금 베어 먹더라도 다른 과자에는 아무런 영향이 없는 것과 마찬가지로 동일한 클래스로 만든 객체들은 서로 전혀 영향을 주지 않는다.

- 파이썬 클래스의 가장 간단한 예

```python
>>> class Cookie:
...     pass
...
>>>
```

- 객체는 클래스로 만들고 1개의 클래스는 무수히 많은 객체를 만들어 낼 수 있다. 
- 위에서 만든 Cookie 클래스의 객체를 만드는 방법은 다음과 같다.

```python
>>> a = Cookie()
>>> b = Cookie()
```

- Cookie()의 결괏값을 리턴받은 a와 b가 바로 객체이다. 마치 함수를 사용해서 그 결괏값을 리턴받는 모습과 비슷하다.

> 객체와 인스턴스의 차이
> 
> 클래스로 만든 객체를 ‘인스턴스’라고도 한다. <code>a = Cookie()</code>로 만든 a는 객체이다. 그리고 a 객체는 Cookie의 인스턴스이다. 즉, 인스턴스라는 말은 특정 객체(a)가 어떤 클래스(Cookie)의 객체인지를 관계 위주로 설명할 때 사용한다. ‘a는 인스턴스’보다 ‘a는 객체’라는 표현이 어울리며 ‘a는 Cookie의 객체’보다 ‘a는 Cookie의 인스턴스’라는 표현이 훨씬 잘 어울린다.

## 사칙 연산 클래스 만들기

### 클래스 구조 만들기

- 제일 먼저 할 일은 a = FourCal()처럼 객체를 만들 수 있게 하는 것이다. 
- 일단은 아무런 기능이 없어도 되기 때문에 매우 간단하게 만들 수 있다.

```python
>>> class FourCal:
...     pass
```

- 먼저 대화형 인터프리터에서 pass라는 문장만을 포함한 FourCal 클래스를 만든다. 
- 현재 상태에서 FourCal 클래스는 아무 변수나 함수도 포함하지 않지만, 우리가 원하는 객체 a를 만들 수 있는 기능은 가지고 있다. 

```python
>>> a = FourCal()
>>> type(a)
<class '__main__.FourCal'>
```

- 위와 같이 <code>a = FourCal()</code>로 a 객체를 먼저 만든 후 type(a)로 a 객체가 어떤 타입인지 알아보았다. 역시 객체 a가 FourCal 클래스의 인스턴스라는 것을 알 수 있다.

> type은 파이썬이 자체로 가지고 있는 내장 함수로, 객체의 타입을 출력한다.

### 객체에 연산할 숫자 지정하기

- 먼저 사칙 연산을 할 때 사용할 2개의 숫자를 a 객체에게 알려 주어야 한다. 
- 다음과 같이 연산을 수행할 대상(4, 2)을 객체에 지정할 수 있게 만들어 보자.

```python
>>> a.setdata(4, 2)
```

- 위 문장이 동작하려면 다음과 같이 FourCal 클래스를 다시 정의해야 한다.

```python
>>> class FourCal:
...     def setdata(self, first, second):
...         self.first = first
...         self.second = second
```

- 앞에서 만든 FourCal 클래스에서 pass 문장을 삭제하고 그 대신 setdata 함수를 정의했다. 
- 클래스 안에 구현된 함수는 다른 말로 메서드(method)라고 부른다.

- 일반적인 함수를 만들 때는 다음과 같이 소스 코드를 작성한다.

```python
def 함수_이름(매개변수):
    수행할_문장
    ...
```

- 메서드도 클래스에 포함되어 있다는 점만 제외하면 일반 함수와 다를 것이 없다.
- setdata 메서드를 다시 보면 다음과 같다.

```python
def setdata(self, first, second):   # 메서드의 매개변수
    self.first = first              # 메서드의 수행문
    self.second = second            # 메서드의 수행문
```

#### setdata 메서드의 매개변수

-  setdata 메서드는 매개변수로 self, first, second 3개의 입력값을 받는다. 
-  일반 함수와 달리, 메서드의 첫 번째 매개변수 self는 특별한 의미를 가진다.
- 다음과 같이 a 객체를 만들고 a 객체를 통해 setdata 메서드를 호출해 보자.

```python
>>> a = FourCal()
>>> a.setdata(4, 2)
```

> 객체를 이용해 클래스의 메서드를 호출하려면 a.setdata(4, 2)와 같이 도트(.) 연산자를 사용하면 된다.

- setdata 메서드에는 self, first, second 총 3개의 매개변수가 필요한데 실제로는 <code>a.setdata(4, 2)</code>처럼 2개의 값만 전달했다.
- <code>a.setdata(4, 2)</code>처럼 호출하면 setdata 메서드의 첫 번째 매개변수 self에는 setdata 메서드를 호출한 객체 a가 자동으로 전달되기 때문이다.
- 파이썬 메서드의 첫 번째 매개변수 이름은 관례적으로 self를 사용한다. 
- 객체를 호출할 때 호출한 객체 자신이 전달되기 때문에 self라는 이름을 사용한 것이다.
- 메서드의 첫 번째 매개변수 self를 명시적으로 구현하는 것은 파이썬만의 독특한 특징이다. 

#### 메서드를 호출하는 또 다른 방법

- 잘 사용하지는 않지만, 다음과 같이 클래스를 이용해 메서드를 호출할 수도 있다.

```python
>>> a = FourCal()
>>> FourCal.setdata(a, 4, 2)
```

- 위와 같이 ‘클래스명.메서드’ 형태로 호출할 때는 객체 a를 첫 번째 매개변수 self에 꼭 전달해야 한다.
- 반면 다음처럼 ‘객체.메서드’ 형태로 호출할 때는 self를 반드시 생략해서 호출해야 한다.

```python
>>> a = FourCal()
>>> a.setdata(4, 2)
```

#### setdata 메서드의 수행문

```python
def setdata(self, first, second):   # 메서드의 매개변수
    self.first = first              # 메서드의 수행문
    self.second = second            # 메서드의 수행문
```

- a.setdata(4, 2)처럼 호출하면 setdata 메서드의 매개변수 first, second에는 각각 값 4와 2가 전달되어 setdata 메서드의 수행문이 다음과 같이 해석된다.

```python
self.first = 4
self.second = 2
```

- self는 전달된 객체 a이므로 다시 다음과 같이 해석된다.

```python
a.first = 4
a.second = 2
```

- <code>a.first = 4</code>라는 문장이 수행되면 a 객체에 객체변수 first가 생성되고 4라는 값이 저장된다. 이와 마찬가지로 <code>a.second = 2</code>라는 문장이 수행되면 a 객체에 객체변수 second가 생성되고 2라는 값이 저장된다.

> 객체에 생성되는 객체만의 변수를 ‘객체변수’ 또는 ‘속성’이라고 부른다.

```python
>>> a = FourCal()
>>> a.setdata(4, 2)
>>> a.first
4
>>> a.second
2
```

- a 객체에 객체변수 first와 second가 생성된 것을 확인할 수 있다.
- 이번에는 다음과 같이 a, b 객체를 만들어 보자.

```python
>>> a = FourCal()
>>> b = FourCal()
```

- a 객체의 객체변수 first를 다음과 같이 생성한다.

```python
>>> a.setdata(4, 2)
>>> a.first
4
```

- b 객체의 객체변수 first를 다음과 같이 생성한다.

```python
>>> b.setdata(3, 7)
>>> b.first
3
```

- 위와 같이 진행하면 b 객체의 객체변수 first에는 값 3이 저장된다는 것을 확인할 수 있었다. 
- a는 원래 값인 4를 유지합니다.

```python
>>> a.first
4
```

- a 객체의 first 값은 b 객체의 first 값에 영향받지 않고 원래 값을 유지하고 있다는 것을 확인할 수 있다. 
- 클래스로 만든 객체의 객체변수는 다른 객체의 객체변수에 상관없이 독립적인 값을 유지한다.
- 다음은 현재까지 완성된 FourCal 클래스이다.

```python
>>> class FourCal:
...     def setdata(self, first, second):
...         self.first = first
...         self.second = second
```

### 더하기 기능 만들기

- 2개의 숫자 값을 설정해 주었으므로 2개의 숫자를 더하는 기능을 방금 만든 클래스에 추가해 보자. 

```python
>>> class FourCal:
...     def setdata(self, first, second):
...         self.first = first
...         self.second = second
...     def add(self):
...         result = self.first + self.second
...         return result
```

```python
>>> a = FourCal()
>>> a.setdata(4, 2)
>>> a.add()
6
```