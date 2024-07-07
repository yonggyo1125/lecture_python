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

|포멧코드|설명| 예                        |
|---|----|--------------------------|
|%a|요일의 줄임말| Mon                      |
|%A|요일| Monday                   |
|%b|달의 줄임말| Jan                      |
|%B|달| January                  |
|%c|날짜와 시간을 출력함.| Thu May 25 10:13:52 2023 |
|%d|일(day)| \[01,31\]                |
|%H|시간(hour): 24시간 출력 형태|\[00:23\]|
|%I|시간(hour): 12시간 출력 형태|\[01:12\]|