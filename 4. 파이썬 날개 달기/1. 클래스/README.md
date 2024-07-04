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