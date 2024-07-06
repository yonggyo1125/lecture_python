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