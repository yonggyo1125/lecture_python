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

### 문자열에 큰따옴표 포함하기

```
"Python is very easy." he says. 
```
- 위와 같이 큰 따옴표가 포함된 문자열이라면 문자열을 작은 따옴표로 둘러싸면 된다.

```python
>>> say = '"Python is very easy." he says.'
```

- 작은 따옴표 안에 사용된 큰 따옴표는 문자열을 만드는 기호로 인식되지 않는다.

### 역슬래시를 사용해서 작은 따옴표와 큰 따옴표를 문자열에 포함하기

```python
>>> food = 'Python\'s favorite food is perl'
>>> say = "\"Python is very easy\" he says."
```

- 작은 따옴표나 큰 따옴표를 문자열에 포함시키는 또 다른 방법은 역슬래스(\)를 사용하는 것이다. 
- 역슬래시를 작은 따옴표나 큰 따옴표 앞에 삽입하면 역슬래시 뒤의 작은 따옴표나 큰 따옴표는 문자열을 둘러싸는 기호의 의미가 아니라 '나 " 자체를 뜻하게 된다.

## 여러 줄인 문자열을 변수에 대입하고 싶을 때

```
Life is too short
You need python
```

### 줄을 바꾸기 위한 이스케이프 코드 \n 삽입하기

```python
>>> multiline = "Life is too short\nYou need python"
```
> 줄바꿈 문자인 \n을 삽입하는 방법이 있지만 읽기가 불편하고 줄이 길어지는 단점이 있다.

### 연속된 작은 따옴표 3개 또는 큰 따옴표 3개 사용하기 

```python
>>> multiline = '''
... Life is too short
... You need python
... '''
```

```python
>>> multiline = """
... Life is too short
... You need python
... """
```

- print(multiline)을 입력하면 다음ㅁ과 같이 출력된다.

```python
>>> print(multiline)
Life is too short
You need python
```

- 문자열이 여러 줄인 경우, 이스케이프 코드를 쓰는 것보다 따옴표 3개를 사용하는 것이 훨씬 깔끔합니다.

> **이스케이프 코드란?**
> 
> 이스케이프(escape) 코드란 프로그래밍할 때 사용할 수 있도록 미리 정의해 둔 '문자 조합'을 말한다. 주로 출력물을 보기 좋게 정렬하는 용도로 사용한다. 몇 가지 이스케이프 코드를 정리하면 다음과 같다.

|코드|설명|
|---|-----|
|\n|문자열 안에서 줄을 바꿀 때 사용|
|\t|문자열 사이에 탭 간격을 줄 때 사용|
|\\|\를 그대로 표현할 때 사용|
|\'|작은 따옴표(')를 그대로 표현할 때 사용|
|\"|큰 따옴표(")를 그대로 표현할 때 사용|
|\r|캐지리 리턴(줄 바꿈 문자, 커서를 현재 줄의 가장 앞으로 이동)|
|\f|폼 피드(줄 마꿈 문자, 커서를 현재 줄의 다음 줄로 이동)|
|\a|벨 소리(출력할 때 PC 스피커에서 '삑' 소리가 난다)|
|\b|백 스페이스|
|\000|널 문자|

## 문자열 연산하기
### 문자열 더해서 연결하기

```python
>>> head = "Python"
>>> tail = " is fun!"
>>> head + tail
'Python is fun!'
```

### 문자열 곱하기

```python
>>> a = "python"
>>> a * 2
'pythonpython'
```
> 위 소스 코드에서 a * 2라는 문장은 a를 2번 반복하라는 뜻

### 문자열 곱하기를 응용하기

> multistring.py

```python
print("=" * 50)
print("My Program")
print("=" * 50)
```

> 프로그램 실행

```python
python multistring.py
```

### 문자열 길이 구하기

```python
>>> a = "Life is too short"
>>> len(a)
17
```

## 문자열 인덱싱과 슬라이싱

- 인덱싱(indexing) : 무엇인가를 '가리킨다'를 의미
- 슬라이싱(slicing) : 무엇인가를 '잘라낸다'라는 의미

### 문자열 인덱싱

```python
>>> a = "Life is too short, You need Python"
```

- "Life is too short, You need Python" 문자열에서 L은 첫 번째 자리를 뜻하는 숫자 0, i는 1 이런식으로 계속 번호를 붙인 것
- 중간에 있는 short의 s는 12가 된다.

```python
>>> a = "Life is too short, You need Python"
>>> a[3]
'e'
```
- 파이썬은 0부터 숫자를 센다.
- a\[3\]이 뜻하는 것은 a라는 문자열의 네 번째 문자 e를 말한다. 