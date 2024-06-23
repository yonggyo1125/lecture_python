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
- a\[번호\]는 문자열 안의 특정한 값을 뽑아 내는 역할을 한다. 
- 이러한 작업을 '인덱싱'이라고 한다. 

### 문자열 인덱싱 활용하기

```python
>>> a = "Life is too short, You need Python"
>>> a[0]
'L'
>>> a[12]
's'
>>> a[-1]
'n'
```

- a\[-1\]이 뜻하는 것은 문자열을 뒤에서부터 읽기 위하여 -(빼기) 기호를 붙인 것이다.
- a\[-1\]은 뒤에서부터 세어 첫 번째가 되는 문자열을 말한다.

```python
>>> a[-2]  # 뒤에서부터 두 번째 문자 
>>> a[-5]  # 뒤에서부터 다섯 번째 문자
```

### 문자열 슬라이싱

```python
>>> a = "Life is too short, You need Python"
>>> b = a[0] + a[1] + a[2] + a[3]
>>> b
'Life'
```

- 위와 같이 단순하게 접근할 수도 있지만 슬라이싱(slicing) 기법으로 다음과 같이 간단하게 처리할 수 있다.

```python
>>> a = "Life is too short, You need Python"
>>> a[0:4]
'Life'
```

- 슬라이싱 기법으로 a\[시작_번호:끝_번호\]를 지정할 때 끝 번호에 해당하는 문자는 포함하지 않습니다. 
- 즉, a\[a:3\]을 수식으로 나타내면 다음과 같습니다.

```
0 <= a < 3
```

### 문자열을 슬라이싱 하는 방법

```python
>>> a[0:5]
'Life '
```

- 공백 문자 역시 L, i, f, e와 같은 문자와 동일하게 취급된다.
- 즉, 'Life'와 'Life '는 완전히 다른 문자열이다.
- 슬라이싱할 때 항상 시작 번호가 0일 필요는 없다.

```python
>>> a[0:2]
'Li'
>>> a[5:7]
'is'
>>> a[12:17]
'short'
```

- a\[시작_번호:끝_번호\]에서 끝 번호 부분을 생략하면 시작 번호부터 그 문자열의 끝까지 뽑아낸다.

```python
>>> a[10:]
'You need Python'
```

- a\[시작_번호:끝_번호\]에서 시작 번호를 생략하면 문자열의 처음부터 끝 번호까지 뽑아 낸다.

```python
>>> a[:17]
'Life is too short'
```

- a\[시작_번호:끝_번호\]에서 시작 번호와 끝 번호를 생략하면 문자열의 처음부터 끝까지 뽑아낸다.

```python
>>> a[:]
'Life is too short, You need Python'
```

- 슬라이싱에서도 인덱싱과 마찬가지로 -(빼기) 기호를 사용할 수 있다.

```python
>>> a[19:-7]
'You need'
```

- a\[19:-7\]은 a\[19\]에서 a\[-8\]까지를 의미한다. 이때에도 a\[-7\]은 포함하지 않는다.

### 슬라이싱으로 문자열 나누기

```python
>>> a = "20230331Rainy"
>>> date = a[:8]
>>> weather = a[8:]
>>> date
'20230331'
>>> weather
'Rainy'
```
- 문자열 a를 두 부분으로 나누는 기법 
- a\[:8\]은 a\[8\]을 포함하지 않고 a\[8:\]은 a\[8\]을 포함하기 때문에 8을 기준으로 해서 두 부분으로 나눌 수 있는 것 

```python
>>> a = "20230331Rainy"
>>> year = a[:4]
>>> day = a[4:8]
>>> weather = a[8:]
>>> year
'2023'
>>> day
'0331'
>>> weather
'Rainy'
```

### Pithon 문자열을 Python으로 바꾸면?

```python
>>> a = "Pithon"
>>> a[1] # a[1]의 값은 i 
'i'
>>> a[1] = 'y'  # 오류 발생
```

- 문자열의 요소값은 바꿀 수 있는 값이 아니기 때문에 오류가 발생한다.
- 문자열을 '변경 불가능한(immutable) 자료형'이라고 부른다.
- 슬라이싱 기법을 사용하면 Pithon 문자열을 사용해 Python문자열을 만들 수 있다.

```python

```