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

- 예시로 유치원생 5명에게 간식을 나누어 주고자 다음과 같은 파이썬 코드를 작성해 보자.

```python
# itertools_zip.py
students = ['한민서', '황지민', '이영철', '이광수', '김승민']
snacks = ['사탕', '초컬릿', '젤리']

result = zip(students, snacks)
print(list(result))
```

- 간식의 개수가 유치원생보다 적으므로 이 파이썬 코드를 실행하면 다음과 같은 결과가 나온다.

```python
[('한민서', '사탕'), ('황지민', '초컬릿'), ('이영철', '젤리')]
```

- students와 snacks의 요소 개수가 다르므로 더 적은 snacks의 개수만큼만 zip()으로 묶게 된다.
- students의 요소 개수가 snacks보다 많을 때 그만큼을 ‘새우깡’으로 채우려면 어떻게 해야 할까? 이럴 때 요소 개수가 많은 것을 기준으로 자료형을 묶는 itertools.zip_longest()를 사용하면 된다. 부족한 항목은 None으로 채우는데, 다음처럼 fillvalue로 값을 지정하면 None 대신 다른 값으로 채울 수 있다.

```python
# itertools_zip.py

students = ['한민서', '황지민', '이영철', '이광수', '김승민']
snacks = ['사탕', '초컬릿', '젤리']

result = itertools.zip_longest(students, snacks, fillvalue='새우깡')
print(list(result))
```

- 실행 결과는 다음과 같다.

```python
[('한민서', '사탕'), ('황지민', '초콜릿'), ('이영철', '젤리'), ('이광수', '새우깡'), ('김승민', '새우깡')]
```

## itertools.permutation

- <code>itertools.permutations(iterable, r)</code>은 반복 가능 객체 중에서 r개를 선택한 순열을 이터레이터로 리턴하는 함수이다.
> 이터레이터란 반복 가능한 객체를 의미한다.

- 1, 2, 3이라는 숫자가 적힌 3장의 카드에서 2장의 카드를 꺼내 만들 수 있는 2자리 숫자를 모두 구하려면 어떻게 해야 할까?
- \[1, 2, 3\]이라는 3장의 카드 중 순서에 상관없이 2장을 뽑는 경우의 수는 모두 3가지이다(조합).

```
1, 2
2, 3
1, 3
```

- 하지만 이 문제에서는 2자리 숫자이므로 이 3가지에 순서를 더해 다음처럼 6가지가 된다(순열).

```
1, 2
2, 1
2, 3
3, 2
1, 3
3, 1
```

- 이 순열은 itertools.permutations()를 사용하면 간단히 구할 수 있다.

```python
>>> import itertools
>>> list(itertools.permutations(['1', '2', '3'], 2))
[('1', '2'), ('1', '3'), ('2', '1'), ('2', '3'), ('3', '1'), ('3', '2')]
```

- 따라서 만들 수 있는 2자리 숫자는 다음과 같이 모두 6가지이다.

```python
>>> for a, b in itertools.permutations(['1', '2', '3'], 2):
...     print(a+b)
...
12
13
21
23
31
32
```

### 조합을 사용하는 함수

- 3장의 카드에서 순서에 상관없이 2장을 고르는 조합은 다음처럼 itertools.combinations()를 사용하면 된다.

```python
>>> import itertools
>>> list(itertools.combinations(['1', '2', '3'], 2))
[('1', '2'), ('1', '3'), ('2', '3')]
```

## itertools.combination

- <code>itertools.combinations(iterable, r)</code>은 반복 가능 객체 중에서 r개를 선택한 조합을 이터레이터로 리턴하는 함수이다.
- 1~45 중 서로 다른 숫자 6개를 뽑는 로또 번호의 모든 경우의 수(조합)를 구하고 그 개수를 출력하려면 어떻게 해야 할까?
- 다음과 같이 itertools.combinations()를 사용하면 45개의 숫자 중 6개를 선택하는 경우의 수를 구할 수 있다.

```python
>>> import itertools
>>> it = itertools.combinations(range(1, 46), 6)
```

- <code>itertools.combinations(range(1, 46), 6)</code>은 1~45의 숫자 중에서 6개를 뽑는 경우의 수를 이터레이터로 리턴한다.
- 이터레이터 객체를 루프를 이용하여 출력하면 아마 끝도 없이 출력될 것이다. 궁금하다면 직접 실행해 봐도 좋다.

```python
**>>> for num in it:
...     print(num)
...
(1, 2, 3, 4, 5, 6)
(1, 2, 3, 4, 5, 7)
(1, 2, 3, 4, 5, 8)
(1, 2, 3, 4, 5, 9)
(1, 2, 3, 4, 5, 10)
(1, 2, 3, 4, 5, 11)
(1, 2, 3, 4, 5, 12)
(1, 2, 3, 4, 5, 13)
...
```

- 하지만 순환하여 출력하지 않고 이터레이터의 개수만 세려면 다음과 같이 하면 된다.

```python
>>> len(list(itertools.combinations(range(1, 46), 6)))
8145060
```
- 선택할 수 있는 로또 번호의 가짓수는 8,145,060이다.


### 중복 조합을 사용하는 함수

- 만약 로또 복권이 숫자 중복을 허용하도록 규칙이 변경된다면 경우의 수는 몇 개가 될까?
> 중복이 허용된다는 것은 당첨 번호가 \[1, 2, 3, 4, 5, 5\]처럼 5가 2번 이상 나와도 되고 \[1, 1, 1, 1, 1, 1\]처럼 1이 6번 나와도 된다는 의미이다.

- 같은 숫자를 허용하는 중복 조합은 itertools.combinations_with_replacement()를 사용하면 된다.

```python
>>> len(list(itertools.combinations_with_replacement(range(1, 46), 6)))
15890700
```

- 당연히 중복을 허용하지 않을 때보다 훨씬 많은 경우의 수가 리턴되는 것을 확인할 수 있다

## functools.reduce

- functools.reduce(function, iterable)은 함수(function)를 반복 가능한 객체(iterable)의 요소에 차례대로(왼쪽에서 오른쪽으로) 누적 적용하여 이 객체를 하나의 값으로 줄이는 함수이다.

- 다음은 입력 인수 data의 요소를 모두 더하여 리턴하는 add 함수이다.

```python
def add(data):
    result = 0
    for i in data:
        result += i
    return result

data = [1, 2, 3, 4, 5]
result = add(data)
print(result)  # 15 출력
```

- functools.reduce()를 사용하여 마찬가지로 동작하는 코드를 작성하려면 어떻게 해야 할까? functools.reduce()를 사용한 코드는 다음과 같다.

```python
# reduce_test.py
import functools

data = [1, 2, 3, 4, 5]
result = functools.reduce(lambda x, y: x + y, data)
print(result)  # 15 출력
```

- functools.reduce()를 사용하면 reduce()에 선언한 람다 함수를 data 요소에 차례대로 누적 적용하여 다음과 같이 계산한다.

```
((((1+2)+3)+4)+5)
```

- 따라서 앞서 본 add 함수와 동일한 역할을 하게 된다.

### functools.reduce()로 최댓값 구하기

- functools.reduce 함수로 최댓값도 구할 수 있다.

```python
num_list = [3, 2, 8, 1, 6, 7]
max_num = functools.reduce(lambda x, y : x if x > y else y, num_list)
print(max_num) # 8 출력
```

- \[3, 2, 8, 1, 6, 7\] 요소를 차례대로 reduce()의 람다 함수로 전달하여 두 값 중 큰 값을 선택하고 마지막에 남은 최댓값을 리턴한다.

> 최솟값은 <code>functools.reduce(lambda x, y: x if x < y else y, num_list)</code>로 구할수 있다.


## operator.itemgetter

- operator.itemgetter는 주로 sorted와 같은 함수의 key 매개변수에 적용하여 다양한 기준으로 정렬할 수 있도록 도와주는 모듈이다.
- 예를 들어 학생의 이름, 나이, 성적 등의 정보를 저장한, 다음과 같은 students 리스트가 있다고 가정해 보자.

```python
students = [
    ("jane", 22, 'A'),
    ("dave", 32, 'B'),
    ("sally", 17, 'B'),
]
```

- students 리스트에는 3개의 튜플이 있으며 각 튜플은 순서대로 이름, 나이, 성적에 해당하는 데이터로 이루어졌다. 이 리스트를 나이순으로 정렬하려면 어떻게 해야 할까?
- 이 문제는 다음처럼 sorted 함수의 key 매개변수에 itemgetter()를 적용하면 쉽게 해결할 수 있다.

```python
# itemgetter1.py
from operator import itemgetter

students = [
  ("jane", 22, 'A'),
  ("dave", 32, 'B'),
  ("sally", 17, 'B'),
]

result = sorted(students, key=itemgetter(1))
print(result)
```

- 이 파일을 실행하여 출력해 보면 다음과 같이 나이 순서대로 정렬한 것을 확인할 수 있다.

```
[('sally', 17, 'B'), ('jane', 22, 'A'), ('dave', 32, 'B')]
```

- itemgetter(1)은 students의 아이템인 튜플의 두 번째 요소를 기준으로 정렬하겠다는 의미이다. 만약 itemgetter(2)와 같이 사용한다면 성적순으로 정렬한다.
- 이번에는 students의 요소가 다음처럼 딕셔너리일 때를 생각해 보자.

```python
students = [
    {"name": "jane", "age": 22, "grade": 'A'},
    {"name": "dave", "age": 32, "grade": 'B'},
    {"name": "sally", "age": 17, "grade": 'B'},
]
```

- 딕셔너리일 때도 마찬가지로 age를 기준으로 정렬해 보자. 이때도 마찬가지로 itemgetter()를 적용하면 된다. 단, 이번에는 <code>itemgetter('age')</code>처럼 딕셔너리의 키를 사용해야 한다. <code>itemgetter('age')</code>는 딕셔너리의 키인 age를 기준으로 정렬하겠다는 의미이다.

```python
# itemgetter2.py
from operator import itemgetter

students = [
  {"name": "jane", "age": 22, "grade": 'A'},
  {"name": "dave", "age": 32, "grade": 'B'},
  {"name": "sally", "age": 17, "grade": 'B'},
]

result = sorted(students, key=itemgetter('age'))
print(result)
```

- 출력 결과는 다음과 같이 age 순으로 정렬된 것을 확인할 수 있다.

```python
[{'name': 'sally', 'age': 17, 'grade': 'B'}, {'name': 'jane', 'age': 22, 'grade': 'A'}, {'name': 'dave', 'age': 32, 'grade': 'B'}]
```

### operator.attrgetter()

- students 리스트의 요소가 튜플이 아닌 Student 클래스의 객체라면 다음처럼 attrgetter()를 적용하여 정렬해야 한다.

```python
# attrgetter1.py
from operator import attrgetter

class Student:
    def __init__(self, name, age, grade):
        self.name = name
        self.age = age
        self.grade = grade

students = [
  Student('jane', 22, 'A'),
  Student('dave', 32, 'B'),
  Student('sally', 17, 'B'),
]

result = sorted(students, key=attrgetter('age'))
```

- <code>attrgetter('age')</code>는 Student 객체의 age 속성으로 정렬하겠다는 의미이다. 이와 마찬가지로 <code>attrgetter('grade')</code>와 같이 사용하면 성적순으로 정렬한다.


## shutil

- shutil은 파일을 복사(copy)하거나 이동(move)할 때 사용하는 모듈이다.
- 작업 중인 파일을 자동으로 백업하는 기능을 구현하고자 c:\doit\a.txt를 c:\temp\a.txt.bak이라는 이름으로 복사하는 프로그램을 만들고자 한다. 
- c:\doit 디렉터리에 a.txt를 만드는 중이며 백업용 c:\temp 디렉터리는 이미 만들었다고 가정한다.
- 다음은 shutil을 사용한 방법이다.

```python
# shutil_copy.py
import shutil

shutil.copy("c:/doit/a.txt", "c:/temp/a.txt.bak")
```

### shutil.move로 삭제 기능 만들기

- 휴지통으로 삭제하는 기능을 구현하고자 c:\doit\a.txt 파일을 c:\temp\a.txt로 이동하려면 다음과 같이 코드를 작성해야 한다.

```python
# shutil_move.py
import shutil

shutil.move("c:/doit/a.txt", "c:/temp/a.txt")
```

## glob

- 가끔 파일을 읽고 쓰는 기능이 있는 프로그램을 만들다 보면 특정 디렉터리에 있는 파일 이름 모두를 알아야 할 때가 있다. 이럴 때 사용하는 모듈이 바로 glob이다.

### 디렉터리에 있는 파일들을 리스트로 만들기 - glob(pathname)

- glob 모듈은 디렉터리 안의 파일들을 읽어서 리턴한다. <code>*</code>, <code>?</code> 등 메타 문자를 써서 원하는 파일만 읽어 들일 수도 있다. 
- 다음은 <code>C:/doit</code> 디렉터리에 있는 파일 중 이름이 mark로 시작하는 파일을 모두 찾아서 읽어들이는 예이다.

> <code>?</code>는 1자리 문자열, <code>*</code>은 임의의 길이의 문자열을 의미한다.

```python
>>> import glob
>>> glob.glob("c:/doit/mark*")
['c:/doit\\marks1.py', 'c:/doit\\marks2.py', 'c:/doit\\marks3.py']
>>>
```

## pickle

- pickle은 객체의 형태를 그대로 유지하면서 파일에 저장하고 불러올 수 있게 하는 모듈이다. 
- 다음 예는 pickle 모듈의 dump 함수를 사용하여 딕셔너리 객체인 data를 그대로 파일에 저장하는 방법을 보여 준다.

```python
>>> import pickle
>>> f = open("test.txt", "wb")
>>> data = {1: 'python', 2: 'you need'}
>>> pickle.dump(data, f)
>>> f.close()
```

- 다음은 pickle.dump로 저장한 파일을 pickle.load를 사용해서 원래 있던 딕셔너리 객체(data) 상태 그대로 불러오는 예이다.

```python
>>> import pickle
>>> f = open("test.txt", "rb")
>>> data = pickle.load(f)
>>> print(data)
{2:'you need', 1:'python'}
```

- 위 예에서는 딕셔너리 객체를 사용했지만, 어떤 자료형이든 저장하고 불러올 수 있다.

## OS

- os 모듈은 환경 변수나 디렉터리, 파일 등의 OS 자원을 제어할 수 있게 해 주는 모듈이다.

### 내 시스템의 환경 변숫값을 알고 싶을 때 - os.environ

- 시스템은 제각기 다른 환경 변숫값을 가지고 있는데, os.environ은 현재 시스템의 환경 변숫값을 리턴한다. 다음을 따라 해 보자.

```python
>>> import os
>>> os.environ
environ({'PROGRAMFILES': 'C:\\Program Files', 'APPDATA': … 생략 …})
```

- os.environ은 환경 변수에 대한 정보를 딕셔너리 형태로 구성된 environ 객체로 리턴한다.
- 리턴받은 객체는 다음과 같이 호출하여 사용할 수 있다.  다음은 PATH 환경 변수 내용이다.

```python
>>> os.environ['PATH']
'C:\\ProgramData\\Oracle\\Java\\javapath;...생략...'
```

### 디렉터리 위치 변경하기 - os.chdir

- os.chdir를 사용하면 다음과 같이 현재 디렉터리의 위치를 변경할 수 있다.

```python
>>> os.chdir("C:\WINDOWS")
```

### 디렉터리 위치 돌려받기 - os.getcwd

- os.getcwd는 현재 자신의 디렉터리 위치를 리턴한다.

```python
>>> os.getcwd()
'C:\WINDOWS'
```

### 시스템 명령어 호출하기 - os.system

- 시스템 자체의 프로그램이나 기타 명령어를 파이썬에서 호출할 수도 있다. <code>os.system("명령어")</code>처럼 사용한다.
- 다음은 현재 디렉터리에서 시스템 명령어 dir을 실행하는 예이다.

```python
>>> os.system("dir")
```

### 실행한 시스템 명령어의 결괏값 돌려받기 - os.popen

- os.popen은 시스템 명령어를 실행한 결괏값을 읽기 모드 형태의 파일 객체로 리턴한다.

```python
>>> f = os.popen("dir")
```

- 읽어 들인 파일 객체의 내용을 보기 위해서는 다음과 같이 하면 된다.

```python
>>> print(f.read())
```

- 이 밖에 유용한 os 관련 함수는 다음과 같다.

|함수|설명|
|---|----|
|os.mkdir(디렉터리)|디렉터리를 생성한다.|
|os.rmdir(디렉터리)|디렉터리를 삭제한다. 단, 디렉터리가 비어 있어야 삭제할 수 있다.|
|os.remove(파일)|파일을 지운다.|
|os.rename(src,dst)|src라는 이름의 파일을 dst라는 이름으로 바꾼다.|

## zipfile

- zipfile은 여러 개의 파일을 zip 형식으로 합치거나 이를 해제할 때 사용하는 모듈이다.
- 다음과 같은 3개의 텍스트 파일이 있다고 가정해 보자.

```
a.txt
b.txt
c.txt
```

- 이 3개의 텍스트 파일을 하나로 합쳐 ‘mytext.zip’이라는 파일을 만들고 이 파일을 원래의 텍스트 파일 3개로 해제하는 프로그램을 만들려면 어떻게 해야 할까?
- zipfile.ZipFile()을 사용하여 해결해 보자.

```python
# zipfile_test.py
import zipfile

# 파일 합치기
with zipfile.ZipFile('mytext.zip', 'w') as myzip:
    myzip.write('a.txt')
    myzip.write('b.txt')
    myzip.write('c.txt')

# 해제하기
with zipfile.ZipFile('mytext.zip') as myzip:
    myzip.extractall()
```

- ZipFile 객체의 write() 함수로 개별 파일을 추가할 수 있고 extreactall() 함수를 사용하면 모든 파일을 해제할 수 있다.
- 합친 파일에서 특정 파일만 해제하고 싶다면 다음과 같이 extract() 함수를 사용하면 된다.

```python
# 특정 파일만 해제하기
with zipfile.ZipFile('mytext.zip') as myzip:
    myzip.extract('a.txt')
```

- 만약 파일을 압축하여 묶고 싶은 경우에는 compression, compresslevel 옵션을 사용할 수 있다.

```python
# 압축하여 묶기
with zipfile.ZipFile('mytext.zip', 'w', compression=zipfile.ZIP_LZMA, compresslevel=9) as myzip:
  (... 생략 ...)
```

- compression에는 4가지 종류가 있다.
  - ZIP_STORED: 압축하지 않고 파일을 zip으로만 묶는다. 속도가 빠르다.
  - ZIP_DEFLATED: 일반적인 zip 압축으로 속도가 빠르고 압축률은 낮다(호환성이 좋다).
  - ZIP_BZIP2: bzip2 압축으로 압축률이 높고 속도가 느리다.
  - ZIP_LZMA: lzma 압축으로 압축률이 높고 속도가 느리다(7zip과 동일한 알고리즘으로 알려져 있다).
- compressionlevel은 압축 수준을 의미하는 숫자값으로, 1~9를 사용한다. 1은 속도가 가장 빠르지만 압축률이 낮고, 9는 속도는 가장 느리지만 압축률이 높다.

## threading

- 컴퓨터에서 동작하고 있는 프로그램을 프로세스(process)라고 한다. 보통 1개의 프로세스는 1가지 일만 하지만, 스레드(thread)를 사용하면 한 프로세스 안에서 2가지 또는 그 이상의 일을 동시에 수행할 수 있다.
- 간단한 예제로 설명을 대신하겠다.

```python
# thread_test.py
import time

def long_task():  # 5초의 시간이 걸리는 함수
    for i in range(5):
        time.sleep(1)  # 1초간 대기한다.
        print("working:%s\n" % i)

print("Start")

for i in range(5):  # long_task를 5회 수행한다.
    long_task()

print("End")
```

- long_task는 수행하는 데 5초의 시간이 걸리는 함수이다. 위 프로그램은 이 함수를 총 5번 반복해서 수행하는 프로그램이다. 이 프로그램은 5초가 5번 반복되므로 총 25초의 시간이 걸린다.
- 하지만 앞에서 설명했듯이 스레드를 사용하면 5초의 시간이 걸리는 long_task 함수를 동시에 실행할 수 있으므로 시간을 줄일 수 있다.
- 다음과 같이 프로그램을 수정해 보자.

```python
# thread_test.py
import time
import threading # 스레드를 생성하기 위해서는 threading 모듈이 필요하다.

def long_task():
    for i in range(5):
        time.sleep(1)
        print("working:%s\n" % i)

print("Start")

threads = []
for i in range(5):
    t = threading.Thread(target=long_task) # 쓰레드를 생성한다. 
    threads.append(t)

for t in threads:
    t.start() # 스레드를 실행한다. 

print("End")
```

- 이와 같이 프로그램을 수정하고 실행해 보면 25초 걸리던 작업이 5초 정도에 수행되는 것을 확인할 수 있다. 
- threading.Thread를 사용하여 만든 스레드 객체가 동시 작업을 가능하게 해 주기 때문이다.
- 하지만 프로그램을 실행해 보면 "Start"와 "End"가 먼저 출력되고 그 이후에 스레드의 결과가 출력되는 것을 확인할 수 있다. 
- 그리고 프로그램이 정상 종료되지 않는다. 우리가 기대하는 것은 "Start"가 출력되고 그다음에 스레드의 결과가 출력된 후 마지막으로 "End"가 출력되는 것이다.
- 이 문제를 해결하기 위해서는 프로그램을 다음과 같이 수정해야 한다.

```python
# thread_test.py
import time
import threading

def long_task():
    for i in range(5):
        time.sleep(1)
        print("working:%s\n" % i)

print("Start")

threads = []
for i in range(5):
    t = threading.Thread(target=long_task)
    threads.append(t)

for t in threads:
    t.start()

for t in threads:
    t.join()  # join으로 스레드가 종료될때까지 기다린다.

print("End")
```

- 스레드의 join 함수는 해당 스레드가 종료될 때까지 기다리게 한다. 따라서 위와 같이 수정하면 우리가 원하던 출력을 보게 된다.

## tempfile

- 파일을 임시로 만들어서 사용할 때 유용한 모듈이 바로 tempfile이다. <code>tempfile.mkstemp()</code>는 중복되지 않는 임시 파일의 이름을 무작위로 만들어서 리턴한다.

```python
>>> import tempfile
>>> filename = tempfile.mkstemp()
>>> filename
'C:\WINDOWS\TEMP\~-275151-0'
```

- tempfile.TemporaryFile()은 임시 저장 공간으로 사용할 파일 객체를 리턴한다. 이 파일은 기본적으로 바이너리 쓰기 모드(wb)를 갖는다. f.close()가 호출되면 이 파일은 자동으로 삭제된다.

```python
>>> import tempfile
>>> f = tempfile.TemporaryFile()
>>> f.close()
```

## traceback

- traceback은 프로그램 실행 중 발생한 오류를 추적하고자 할 때 사용하는 모듈이다.
- 다음과 같은 코드를 작성하여 실행해 보자.

```python
# traceback_test.py
def a():
    return 1/0

def b():
    a()

def main():
    try:
        b()
    except:
        print("오류가 발생했습니다.")

main()
```

- 프로그램 실행 결과는 다음과 같다.

```
오류가 발생했습니다.
```

- main() 함수가 시작되면 b() 함수를 호출하고 b() 함수에서 다시 a() 함수를 호출하여 1을 0으로 나누므로 오류가 발생하여 "오류가 발생했습니다."라는 메시지를 출력했다.
- 이렇게 간단한 프로그램이 아니라 복잡한 파이썬 코드라면 어디에서 어떤 오류가 발생하는지 알기 어렵다.
- 이때 이 코드에서 오류가 발생한 위치와 원인을 정확히 판단할 수 있도록 코드를 업그레이드하려면 어떻게 해야 할까?
- 오류가 발생한 위치에 다음과 같이 traceback 모듈을 적용해 보자.

```python
# traceback_test.py
import traceback

def a():
    return 1/0

def b():
    a()

def main():
    try:
        b()
    except:
        print("오류가 발생했습니다.")
        print(traceback.format_exc())

main()
```

- 오류가 발생한 위치에 print(traceback.format_exc()) 문장을 추가했다. traceback 모듈의 format_exc()는 오류 추적 결과를 문자열로 리턴하는 함수이다. 이렇게 코드를 수정하고 다시 프로그램을 실행하면 다음과 같이 출력될 것이다.

```
오류가 발생했습니다.
Traceback (most recent call last):
  File "c:\doit\traceback_sample.py", line 14, in main
    b()
  File "c:\doit\traceback_sample.py", line 9, in b
    a()
  File "c:\doit\traceback_sample.py", line 5, in a
    return 1/0
ZeroDivisionError: division by zero
```

- 오류 추적을 통해 main() 함수에서 b() 함수를 호출하고 b() 함수에서 다시 a() 함수를 호출하여 1 / 0을 실행하려 하므로 0으로 나눌 수 없다는 ZeroDivisionError가 발생했다는 것을 로그를 통해 정확하게 확인할 수 있다.

## json

- json은 JSON 데이터를 쉽게 처리하고자 사용하는 모듈이다.
- 다음은 개인정보를 JSON 형태의 데이터로 만든 myinfo.json 파일이다.

```json
{
    "name": "홍길동",
    "birth": "0525",
    "age": 30
}
```

- JSON 파일을 읽어 딕셔너리로 변환하려면 다음처럼 json 모듈을 사용하면 된다.

```python
>>> import json
>>> with open('myinfo.json') as f:
...     data = json.load(f)
...
>>> type(data)
<class 'dict'>
>>> data
{'name': '홍길동', 'birth': '0525', 'age': 30}
```

- JSON 파일을 읽을 때는 이 예처럼 <code>json.load(파일_객체)</code>를 사용한다. 이렇게 load() 함수는 읽은 데이터를 딕셔너리 자료형으로 리턴한다. 
- 이와 반대로 딕셔너리 자료형을 JSON 파일로 생성할 때는 다음처럼 <code>json.dump(딕셔너리, 파일_객체)</code>를 사용한다.

```python
>>> import json
>>>  data = {'name': '홍길동', 'birth': '0525', 'age': 30}
>>> with open('myinfo.json', 'w') as f:
...     json.dump(data, f)
```

- 이번에는 파이썬 자료형을 JSON 문자열로 만드는 방법에 대해서 알아보자.

```python
>>> import json
>>> d = {"name":"홍길동", "birth":"0525", "age": 30}
>>> json_data = json.dumps(d)
>>> json_data
'{"name": "\\ud64d\\uae38\\ub3d9", "birth": "0525", "age": 30}'
```

- 딕셔너리 자료형을 JSON 문자열로 만들려면 json.dumps() 함수를 사용하면 된다. 그런데 딕셔너리를 JSON 데이터로 변경하면 ‘홍길동’과 같은 한글 문자열이 코드 형태로 표시된다. 왜냐하면 dump(), dumps() 함수는 기본적으로 데이터를 아스키 형태로 저장하기 때문이다. 유니코드 문자열을 아스키 형태로 저장하다 보니 한글 문자열이 마치 깨진 것처럼 보인다.
- 그러나 JSON 문자열을 딕셔너리로 다시 역변환하여 사용하는 데는 전혀 문제가 없다. JSON 문자열을 딕셔너리로 변환할 때는 다음처럼 json.loads() 함수를 사용한다.

```python
>>> json.loads(json_data)
{'name': '홍길동', 'birth': '0525', 'age': 30}
```

- 한글 문자열이 아스키 형태의 문자열로 변경되는 것을 방지하는 방법도 있다.

```python
>>> d = {"name":"홍길동", "birth":"0525", "age": 30}
>>> json_data = json.dumps(d, ensure_ascii=False)
>>> json_data
'{"name": "홍길동", "birth": "0525", "age": 30}'
>>> json.loads(json_data)
{'name': '홍길동', 'birth': '0525', 'age': 30}
```

- 이처럼 <code>ensure_ascii=False</code> 옵션을 사용하면 된다. 이 옵션은 데이터를 저장할 때 아스키 형태로 변환하지 않겠다는 뜻이다.
- 출력되는 JSON 문자열을 보기 좋게 정렬하려면 다음처럼 indent 옵션을 추가하면 된다.

```python
>>> d = {"name":"홍길동", "birth":"0525", "age": 30}
>>> print(json.dumps(d, indent=2, ensure_ascii=False))
{
  "name": "홍길동",
  "birth": "0525",
  "age": 30
}
```

- 그리고 딕셔너리 외에 리스트나 튜플처럼 다른 자료형도 JSON 문자열로 바꿀 수 있다.

```python
>>> json.dumps([1,2,3])
'[1, 2, 3]'
>>> json.dumps((4,5,6))
'[4, 5, 6]'
```

## urllib

- urllib은 URL을 읽고 분석할 때 사용하는 모듈이다.
- URL을 호출하여 원하는 리소스를 얻으려면 urllib 모듈을 사용해야 한다.

```python
# urllib_test.py
import urllib.request

def get_wikidocs(page):
    resource = 'https://wikidocs.net/{}'.format(page)
    with urllib.request.urlopen(resource) as s:
        with open('wikidocs_%s.html' % page, 'wb') as f:
            f.write(s.read())
```


### SSL 오류가 발생하면
- get_wikidocs 함수 실행시 다음과 같은 오류가 발생할 수 있다.

```
urllib.error.URLError: <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed
```

- 이 오류는 SSL 인증서 검증에 실패했음을 나타낸다. 파이썬이 서버의 SSL 인증서를 신뢰할 수 있는지 확인하는 과정에서, 로컬 시스템에 필요한 CA(인증 기관) 인증서가 없거나 찾을 수 없어 발생한 문제로 이는 특히 macOS에서 자주 발생하는 문제이다.
- 만약 이와 같은 오류가 발생한다면 다음과 같은 코드를 추가하여 이 문제를 회피할수 있다.

```python
import urllib.request

# SSL 인증서 검증을 비활성화하는 Context 생성
import ssl
context = ssl._create_unverified_context()

def get_wikidocs(page):
    resource = f'https://wikidocs.net/{page}'
    with urllib.request.urlopen(resource, context=context) as s:  # 생성한 Context 전달
        with open(f'wikidocs_{page}.html', 'wb') as f:
            f.write(s.read())

get_wikidocs(12)
```

## webbrowser

- webbrowser는 파이썬 프로그램에서 시스템 브라우저를 호출할 때 사용하는 모듈이다.
- 파이썬으로 웹 페이지를 새 창으로 열려면 webbrowser 모듈의 open_new() 함수를 사용해야 한다.\

```python
# webbrowser_test.py
import webbrowser

webbrowser.open_new('http://python.org')
```

- 이미 열린 브라우저로 원하는 사이트를 열고 싶다면 다음처럼 open_new() 대신 open()을 사용하면 된다

```python
webbrowser.open('http://python.org')
```