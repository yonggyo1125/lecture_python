# 표준 라이브러리

- 파이썬 표준 라이브러리는 파이썬을 설치할 때 자동으로 컴퓨터에 설치된다.
- sys, re 모듈은 파이썬의 중요한 표준 라이브러리이다.


## datetime.date

- datetime.date는 연, 월, 일로 날짜를 표현할 때 사용하는 함수이다.
- 만약 A 군과 B 양이 2021년 12월 14일부터 만나기 시작했다면 2023년 4월 5일은 둘이 사귄 지 며칠째 되는 날일까? 아울러 사귀기 시작한 2021년 12월 14일은 무슨 요일이었을까? datetime.date 함수를 사용하면 이 문제를 쉽게 해결할 수 있다.
- 연, 월, 일로 다음과 같이 datetime.date 객체를 만들 수 있다.

```python
>>> import datetime
>>> day1 = datetime.date(2021, 12, 14)
>>> day2 = datetime.date(2023, 4, 5)
```

- 두 날짜의 차이는 다음과 같이 뺄셈으로 쉽게 구할 수 있다.

```python
>>> diff = day2 - day1
>>> diff.days
477
```

- day2에서 day1을 빼면 datetime 모듈의 timedelta 객체가 리턴된다. 이 객체를 diff 변수에 대입하고 이 diff 변수를 이용하여 두 날짜의 차이를 쉽게 확인해 봤다.
- 요일은 datetime.date 객체의 weekday 함수를 사용하면 쉽게 구할 수 있다.

```python
>>> day = datetime.date(2021, 12, 14)
>>> day.weekday()
1
```

- 0은 월요일을 의미하며 순서대로 1은 화요일, 2는 수요일, …, 6은 일요일이 된다. 
- 이와 달리 월요일은 1, 화요일은 2, …, 일요일은 7을 리턴하려면 다음처럼 isoweekday 함수를 사용하면 된다.

```python
>>> day.isoweekday()
2
```

- 2021년 12월 14일은 화요일이므로 isoweekday()를 사용하면 화요일을 뜻하는 2가 리턴된다. weekday()를 사용하면 1이 리턴된다.

## time

### time.time

- time.time()은 UTC(universal time coordinated, 협정 세계 표준시)를 사용하여 현재 시간을 실수 형태로 리턴하는 함수이다. 1970년 1월 1일 0시 0분 0초를 기준으로 지난 시간을 초 단위로 리턴해 준다.

```python
>>> import time
>>> time.time()
1684983953.5221913
```

### time.localtime

- time.localtime은 time.time()이 리턴한 실숫값을 사용해서 연, 월, 일, 시, 분, 초, ... 의 형태로 바꾸어 주는 함수이다.


```python
>>> time.localtime(time.time())
time.struct_time(tm_year=2023, tm_mon=5, tm_mday=21, tm_hour=16,
    tm_min=48, tm_sec=42, tm_wday=1, tm_yday=141, tm_isdst=0)
```

### time.asctime

- time.asctime은 time.localtime가 리턴된 튜플 형태의 값을 인수로 받아서 날짜와 시간을 알아보기 쉬운 형태로 리턴하는 함수이다.

```python
>>> time.asctime(time.localtime(time.time()))
'Fri Apr 28 20:50:20 2023'
```

### time.ctime

- <code>time.asctime(time.localtime(time.time()))</code>은 간단하게 time.ctime()으로 표시할 수 있다.
- ctime이 asctime과 다른 점은 항상 현재 시간만을 리턴한다는 점이다.

```python
>>> time.ctime()
'Fri Apr 28 20:56:31 2023'
```

### time.strftime

- strftime 함수는 시간에 관계된 것을 세밀하게 표현하는 여러 가지 포맷 코드를 제공한다

```python
time.strftime('출력할 형식 포맷 코드', time.localtime(time.time()))
```

- 시간에 관계된 것을 표현하는 포맷 코드

| 포멧코드 |설명| 예                        |
|------|----|--------------------------|
| %a   |요일의 줄임말| Mon                      |
| %A   |요일| Monday                   |
| %b   |달의 줄임말| Jan                      |
| %B   |달| January                  |
| %c   |날짜와 시간을 출력함.| Thu May 25 10:13:52 2023 |
| %d   |일(day)| \[01,31\]                |
| %H   |시간(hour): 24시간 출력 형태|\[00:23\]|
| %I   |시간(hour): 12시간 출력 형태|\[01:12\]|
| %j   |1년 중 누적 날짜|\[001,366\]|
| %m|달|\[01,12\]|
|%M|분|\[01,59\]|
|%p|AM or PM|AM|
|%S|초|\[00,59\]|
|%U|1년 중 누적 주(일요일 시작)|\[00,53\]|
|%w|숫자로 된 요일|\[0(일), 6(토)\]|
|%W|1년 중 누적 주(월요일 시작)|\[00,53\]|
|%x|현재 설정된 지역에 기반한 날짜 출력|05/25/23|
|%X|현재 설정된 지역에 기반한 시간 출력|17:22:21|
|%Y|연도 출력|2023|
|%Z|시간대 출력|대한민국 표준시|
|%%|문자 %|%|
|%y|세기 부분을 제외한 연도 출력|01|

- 다음은 time.strftime을 사용하는 예이다.

```python
>>> import time
>>> time.strftime('%x', time.localtime(time.time()))
'05/25/23'
>>> time.strftime('%c', time.localtime(time.time()))
'Thu May 25 10:13:52 2023
```

### time.sleep

- time.sleep 함수는 주로 루프 안에서 많이 사용한다. 이 함수를 사용하면 일정한 시간 간격을 두고 루프를 실행할 수 있다.

```python
# sleep1.py
import time
for i in range(10):
    print(i)
    time.sleep(1)
```

- 위 예는 1초 간격으로 0부터 9까지의 숫자를 출력한다. time.sleep 함수의 인수는 실수 형태를 쓸 수 있다. 즉 1이면 1초, 0.5면 0.5초가 되는 것이다.


### 인수 없이 time 함수 사용하기

- time.localtime, time.asctime, time.strftime 함수는 다음처럼 입력 인수 없이 사용할 수 있다. 입력 인수 없이 사용할 경우 현재 시각을 기준으로 함수가 수행된다.

```python
>>> time.localtime()
time.struct_time(tm_year=2023, tm_mon=6, tm_mday=18, tm_hour=17, tm_min=1, tm_sec=4, tm_wday=6, tm_yday=169, tm_isdst=0)
>>> time.asctime()
'Sun Jun 18 17:01:09 2023'
>>> time.strftime('%c')
'Sun Jun 18 17:01:30 2023'
```

## math.gcd

- math.gcd 함수를 이용하면 최대 공약수(gcd, greatest common divisor)를 쉽게 구할 수 있다.
    - math.gcd 함수는 파이썬 3.5 버전부터 사용할 수 있다.
    - 공약수란 두 수 이상의 여러 수의 공통된 약수를 말하며 공약수 중 가장 큰 수를 최대 공약수라고 말한다. 
    - 예를 들어 30과 15의 약수는 1, 3, 5, 15, 최대 공약수는 15이다.
- 어린이집에서 사탕 60개, 초콜릿 100개, 젤리 80개를 준비했다. 아이들이 서로 싸우지 않도록 똑같이 나누어 봉지에 담는다고 하면 최대 몇 봉지까지 만들 수 있을까? 단, 사탕, 초콜릿, 젤리는 남기지 않고 모두 담도록 한다.
- 이 문제는 60, 100, 80의 최대 공약수를 구하면 바로 해결된다. 즉, 똑같이 나눌 수 있는 봉지 개수가 최대가 되는 수를 구하면 된다.

```python
>>> import math
>>> math.gcd(60, 100, 80)
20
```

> 파이썬 3.9 버전부터는 math.gcd에 여러 개의 인수를 입력할 수 있지만, 3.9 미만 버전에서는 2개까지만 허용된다.

- math.gcd() 함수로 최대 공약수를 구했더니 20이었다. 따라서 최대 20봉지를 만들 수 있다. 각 봉지에 들어가는 사탕, 초콜릿, 젤리의 개수는 다음과 같이 전체 개수를 최대 공약수 20으로 나누면 구할 수 있다.

```python
>>> 60/20, 100/20, 80/20
(3.0, 5.0, 4.0)
```

- 따라서 한 봉지당 사탕 3개씩, 초콜릿 5개씩, 젤리 4개씩 담으면 된다.

## math.lcm

- math.lcm은 최소 공배수(lcm, least common multiple)를 구할 때 사용하는 함수이다.
  - math.lcm() 함수는 파이썬 3.9 버전부터 사용할 수 있다.
  - 최소 공배수란 두 수의 공통 배수 중 가장 작은 수를 말한다. 예를 들어 3과 5의 최소 공배수는 15이다.
- 어느 버스 정류장에 시내버스는 15분마다 도착하고 마을버스는 25분마다 도착한다고 한다. 오후 1시에 두 버스가 동시에 도착했다고 할 때 두 버스가 동시에 도착할 다음 시각을 알려면 어떻게 해야 할까?
- 이 문제는 15와 25의 공통 배수 중 가장 작은 수, 즉 최소 공배수를 구하면 바로 해결된다.

```python
>>> import math
>>> math.lcm(15, 25)
75
```

- math.lcm 함수를 사용하여 최소 공배수 75를 구했다. 따라서 두 버스가 동시에 도착할 다음 시각은 75분 후인 오후 2시 15분이다.

## random

- random은 난수(규칙이 없는 임의의 수)를 발생시키는 모듈이다.
- 다음은 0.0에서 1.0 사이의 실수 중에서 난수 값을 리턴하는 예를 보여 준다.

```python
>>> import random
>>> random.random()
0.53840103305098674
```

- 다음 예는 1에서 10 사이의 정수 중에서 난수 값을 리턴해 준다.

```python
>>> random.randint(1, 10)
6
```

- 다음 예는 1에서 55 사이의 정수 중에서 난수 값을 리턴해 준다.

```python
>>> random.randint(1, 55)
43
```

- random 모듈을 사용해서 재미있는 함수를 하나 만들어 보자.

```python
# random_pop.py
import random
def random_pop(data):
  number = random.randint(0, len(data) -1)
  return data.pop(number)

if __name__ == "__main__":
    data = [1, 2, 3, 4, 5]
    while data:
        print(random_pop(data))
```

- 실행 결과

```
2 
3 
1 
5 
4
```

- 앞에서 만든 random_pop 함수는 리스트의 요소 중에서 무작위로 하나를 선택하여 꺼낸 다음 그 값을 리턴한다. 
- 물론 꺼낸 요소는 pop 메서드에 의해 사라진다.
- random_pop 함수는 random 모듈의 choice 함수를 사용하여 다음과 같이 좀 더 직관적으로 만들 수도 있다.

```python
def random_pop(data):
    number = random.choice(data)
    data.remove(number)
    return number
```

- random.choice 함수는 입력으로 받은 리스트에서 무작위로 하나를 선택하여 리턴한다.
- 리스트의 항목을 무작위로 섞고 싶을 때는 random.sample 함수를 사용하면 된다.

```python
>>> import random
>>> data = [1, 2, 3, 4, 5]
>>> random.sample(data, len(data))
[5, 1, 3, 4, 2]
```

- andom.sample 함수에서 두 번째 인수인 <code>len(data)</code>는 무작위로 추출할 원소의 개수를 의미한다. 만약 <code>random.sample(data, 3)</code>과 같이 사용한다면 data 리스트에서 무작위로 3개를 추출하여 리턴할 것이다.

## itertools.zip_longest

- <code>itertools.zip_longest(*iterables, fillvalue=None)</code> 함수는 같은 개수의 자료형을 묶는 파이썬 내장 함수인 zip 함수와 똑같이 동작한다. 하지만 <code>itertools.zip_longest()</code> 함수는 전달한 반복 가능 객체(<code>*iterables</code>)의 길이가 서로 다르다면 긴 객체의 길이에 맞춰 fillvalue에 설정한 값을 짧은 객체에 채울 수 있다.