# 문자열 자료형

- 문자열(String) : 문자, 단어 등으로 구성된 집합
- 따옴표(",')로 둘러싸여 있으면 모두 문자열

```python
"Life is too short, You need Python"
"a"
"123"
```

## 문자열을 만들고 사용하기

1. 큰 따옴표로 양쪽 둘러싸기

```python
"Hello World"
```

2. 작은 따옴표로 둘러싸기

```python
"Pyhon is fun"
```


3. 큰 따옴표 3개를 연속으로 써서 양쪽 둘러싸기

```python
"""Life is too short, You need pyhon"""
```

4. 작은 따옴표 3개를 연속으로 싸서 양쪽 둘러싸기

```python
'''Life is too short, You need python'''
```

## 문자열 안에 작은 따옴표나 큰 따옴표를 포함시키고 싶을 때 

- 문자열 안에도 작은 따옴표와 큰따옴표가 들어 있어야 할 경우가 있다.

### 문자열에 작은따옴표 포함하기

```
Python's favorite food is perl
```


- 이 경우에는 문자열을 큰 따옴표로 둘러싸야 한다. 큰 따옴표 안에 들어 있는 작은 따옴표는 문자열을 나타내기 위한 기호로 인식되지 않는다. 

```python
>>> food = "Python's favorite food is perl"
```

- 프롬프트에 'food'를 입력해서 결과를 확인해 보면 변수에 저장된 문자열이 그대로 출력되는 것을 볼 수 있다.

```python
>>> food
"Python's favorite food is perl"
```

- 시험삼아 다음과 같이 문자열을 큰 따옴표가 아닌 작은 따옴표로 둘러싼 후 다시 실행해보면 'Python'이 문자열로 인식되어 구문 오류(SyntaxError)가 발생할 것이다.