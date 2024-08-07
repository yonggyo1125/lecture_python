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
| \\\\ | \\를 그대로 표현할 때 사용|
|\\'|작은 따옴표(')를 그대로 표현할 때 사용|
|\\"|큰 따옴표(")를 그대로 표현할 때 사용|
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
>>> a = "Pithon"
>>> a[:1]
'P'
>>> a[2:]
'thon'
>>> a[:1] + 'y' + a[2:]
'Pyhon'
```
> 슬라이싱을 사용하면 "Pithon" 문자열을 'P' 부분과 'thon' 부분으로 나눌 수 있고, 그 사이에 'y' 문자를 추가하면 'Python' 이라는 새로운 문자열을 만들 수 있다.

## 문자열 포매팅이란?

- 문자열 안의 특정한 값을 바꿔야 할 경우가 있을 때 이것을 가능하게 해주는 것
- 문자열 안에 어떤 값을 삽입하는 방법

## 문자열 포매팅 따라 하기
### 숫자 바로 대입

```python
>>> "I eat %d apples." % 3
'I eat 3 apples.'
```

- 문자열 안의 숫자를 넣고 싶은 자리에 %d 문자를 넣어 주고 삽입할 숫자 3은 가장 뒤에 있는 % 문자 다음에 써 넣었다. 
- 여기에서 %d는 '문자열 포맷 코드'라고 부른다.

### 문자열 바로 대입

```python
>>> "I eat %s apples." % "five"
'I eat five apples.'
```

- 숫자를 넣기 위해서는 %d, 문자열을 넣기 위해서는 %s를 써야 한다.

### 숫자 값을 나타내는 변수로 대입

```python
>>> number = 3
>>> "I eat %d apples." % number
'I eat 3 apples.'
```

### 2개 이상의 값 넣기

```python
>>> number = 10
>>> day = "three"
>>> "I ate %d apples. so I was sick for %s days." % (number, day)
'I ate 10 apples. so I was sick for three days'
```

- 2개 이상의 값을 넣으려면 마지막 % 다음 괄호 안에 쉼표(,)로 구분하여 각각의 값을 넣어 주면 된다.

## 문자열 포맷 코드

- 문자열 포매팅 예제에서 대입해 넣는 자료형으로 정수의 문자열을 사용했지만, 이 밖에도 다양한 것을 대입할 수 있다.
- 문자열 포맷 코드의 종류는 다음과 같다.

|코드| 설명               |
|---|------------------|
|%s|문자열(string)       |
|%c|문자 1개(character)  |
|%d|정수(integer)       |
|%f|부동소수(floating-point) |
|%o|8진수|
|%x|16진수|
|%%|문자 % 자체|

- %s 포맷 코드는 어떤 형태의 값이든 변환해 넣을 수 있습니다. 

```python
>>> "I have %s apples" % 3
'I have 3 apples'
>>> "rate is %s" % 3.234
'rate is 3.234'
```

- 3을 문자열 안에 삽입하려면 %d를 사용해야 하고 3.234를 삽입하려면 %f를 사용해야 한다. 
- %s를 사용하면 %s는 자동으로 %뒤에 있는 3이나 3.234와 같은 값을 문자열로 바꾸어 대입하기 때문에 이런 것을 생각하지 않아도 된다.

### 포매팅 연산자 %d와 %를 같이 쓸 때는 %%를 쓴다.

```python
>>> "Error is %d%." % 98
```

- 예상과 다르게 파이썬은 '형식이 불완전하다'라는 오류 메시지를 보여 준다.
- 그 이유는 '문자열 포맷 코드인 %d와 %가 같은 문자열 안에 존재하는 경우 %를 나타내려면 반드시 %%를 써야 한다'라는 법칙이 있기 때문이다.
- 문자열 안에 %d와 같은 포매팅 연산자가 없으면 %는 홀로 쓰여도 상관없다. 

```python
>>>  "Errror is %d%%." % 98
'Error is 98%'
```

## 포맷 코드와 숫자 함게 사용하기

### 정렬과 공백 

```python
>>> "%10s" % "hi" # hi가 오른쪽에 정렬됨
'        hi'  
```

- %10s :  전체 길이가 10개인 문자열 공간에서 대입되는 값을 오른족으로 정렬하고 그 앞의 나머지는 공백으로 남겨두라는 의미

```python
>>> "%-10sjane." % 'hi' # hi가 왼쪽 정렬됨.
'hi        jane.' 
```

- hi를 왼쪽으로 정렬하고 나머지는 공백으로 채우라는 것을 의미

### 소수점 표현하기

```python
>>> "%10.4f" % 3.42134234
'3.4213'
```

- 3.42134234를 소수점 네 번째 자리까지만 나타내고 싶은 경우에는 위와 같이 작성한다. 
- %0.4f에서 '.'는 소수점 포인트, 그 뒤의 숫자 4는 소수점 뒤에 나올 숫자의 개수를 말한다. 
- 소수점 포인트 앞의 숫자는 문자열의 전체 길이를 의미하는데, %0.4f에서 사용한 숫자 0은 길이에 상관하지 않겠다는 의미이다.

```python
>>> "%10.4f" % 3.42134234
'    3.4213'
```

- 숫자 3.42134234를 소수점 네 번째 자리까지만 표시하고 전체 길이가 10개인 문자열 공간에서 오른쪽으로 정렬하는 예

## format 함수를 사용한 포매팅

### 숫자 바로 대입하기

```python
>>> "I eat {0} apples".format(3)
'I eat 3 apples'
```

- "I eat {0} apples" 문자열 중 {0} 부분이 숫자 3으로 바뀌었다.

### 문자열 바로 대입하기

```python
>>> "I eat {0} apples".format("five")
'I eat five apples'
```

- 문자열의 {0} 항목이 'five'라는 문자열로 바뀌었다.

### 숫자 값을 가진 변수로 대입하기

```python
>>> number = 3
>>> "I eat {0} apples".format(number)
'I eat 3 apples'
```

### 2개 이상의 값 넣기

```python
>>> number = 10
>>> day = "three"
>> "I ate {0} apples. so I was sick for {1} days.".format(number, day)
'I ate 10 apples. so I was sick for three days.'
```
- {0}은 format 함수의 첫 번째 입력값인 number, {1}은 format 함수의 두 번째 입력값인 day로 바뀐다.

### 이름으로 넣기

```python
>>> "I ate {number} apples. so I was sick for {day} days.".format(number=10, day=3)
'I ate 10 apples. so I was sick for 3 days.'
```

- {name} 형태를 사용할 경우, format 함수에는 반드시 name=value와 같은 형태의 입력값이 있어야 한다. 
- 문자열의 {number}, {day}가 format 함수의 입력값인 number = 10, day = 3값으로 각각 바뀌는 것을 보여준다.

### 인덱스와 이름을 혼용해서 넣기

```python
>>> "I ate {0} apples. so I was sick for {day} days.".format(10, day=3)
'I ate 10 apples. so I was sick for 3 days.'
```

### 왼쪽 정렬

```python
>>> "{0:<10}".format("hi")
'hi        '
```

- **:\<10** - 표현식을 사용하면 문자열을 왼쪽으로 정렬하고 문자열의 총 자릿수를 10으로 맞춘다.

### 오른쪽 정렬

```python
>>> "{0:>10}".format("hi")
'        hi'
```
- 오른쪽 정렬은 :\< 대신 :\>을 사용하면 된다.

### 가운데 정렬

```python
>>> "{0:^10}".format("hi")
'    hi    '
```

### 공백 채우기

```python
>>> "{0:=^10}".format("hi")
'====hi===='
>>> "{0:!<10}".format("hi")
'hi!!!!!!!!'
```

### 소수점 표현하기

```python 
>>> y = 3.42134234
>>> "{0:0.4f}".format(y)
'3.4213'
```

```python
>>> "{0:10.4f}".format(y)
'    3.4213'
```

### { 또는 } 문자 표현하기

```python
>>> "{{ and }}".format()
'{ and }'
```

## f 문자열 포매팅

- 파이썬 3.6 버전 부터는 f문자열 포매팅 기능을 사용할 수 있다.  
- 문자열 앞에 f 접두사를 붙이면 f문자열 포매팅 기능을 사용할 수 있다. 

```python
>>> name = '홍길동'
>>> age = 30
>>> f'나의 이름은 {name}입니다. 나이는 {age}입니다.'
'나의 이름은 홍길동입니다. 나이는 30입니다.'
```

- f 문자열 포매팅은 표현식을 지원하기 때문에 다음과 같은 것도 가능

```python
>>> age = 30
>>> f'나는 내년이면 {agre + 1}살이 된다.'
'나는 내년이면 31살이 된다.'
```

- 딕셔너리는 f문자열 포매팅에서 다음과 같이 사용할 수 있다. 

```python
>>> d = {'name': '홍길동', 'age': 30}
>>> f'나의 이름은 {d["name"]}입니다. 나이는 {d["age"]}입니다.'
'나의 이름은 홍길동입니다. 나이는 30입니다.'
```

- 정렬 

```python
>>> f'{"hi":<10}'    # 왼쪽 정렬
'hi        '
>>> f'{"hi":>10}'    # 오른쪽 정렬
'        hi'
>>> f'{"hi":^10}'   # 가운데 정렬
'    hi    '
```

- 공백 채우기

```python
>>> f'{"hi":=^10}'   # 가운데 정렬하고 '='로 공백 채우기
'====hi===='
>>> f'{"hi":!<10}'   # 왼쪽 정렬하고 '!'로 공백 채우기
'hi!!!!!!!!'
```

- 소수점

```python
>>> y = 3.42134234
>>> f'{y:0.4f}'   # 소수점 4자리까지만 표현
'3.4123'
>>> f'{y:10.4f}'  # 소수점 4자리까지만 표현하고 총 자릿수를 '10'으로 맞춤.
```

- f 문자열에서 {}를 문자 그대로 표시하려면 다음과 같이 2개를 동시에 사용해야 한다.

```python
>>> f'{{ and }}'
'{ and }'
```

## 문자열 관련 함수들 
- 문자열 내장 함수
- 내장 함수를 사용하려면 문자열 변수 이름 뒤에 '.'을 붙인 후 함수 이름을 써준다. 

### 문자 개수 세기 - count

```python
>>> a = "hobby"
>>> a.count('b')
2
```

### 위치 알려 주기 1 - find

```python
>>> a = "Python is the best choice"
>>> a.find('b')  # 문자열에서 b가 처음 나온 위치
14 
>>> a.find('k')  # 찾는 문자나 문자열이 존재하지 않는다면 -1 반환
-1
```

### 위치 알려 주기 2 - index

```python
>>> a = "Life is too short"
>>> a.index('t')
8
>>> a.index('k')   # k가 없으므로 오류 발생
```

- find 함수와 다른 점은 문자열 안에 존재하지 않는 문자를 찾으면 오류가 발생한다는 것

### 문자열 삽입 - join

```python
>>> ",".join('abcd')
'a,b,c,d'
```

- join 함수는 문자열뿐만 아니라 리스트나 튜플도 입력으로 사용할 수 있다. 
- join 함수의 입력으로 리스트를 사용한 예

```python
>>> ",".join(['a', 'b', 'c', 'd'])
'a,b,c,d'
```

### 소문자를 대문자로 바꾸기 - upper

```python
>>> a = "hi"
>>> a.upper()
'HI'
```

### 대문자를 소문자로 바꾸기 - lower

```python
>>> a = "HI"
>>> a.lower()
'hi'
```

### 왼쪽 공백 지우기 - lstrip

```python
>>> a = " hi "
>>> a.lstrip()
'hi '
```

### 오른쪽 공백 지우기 - rstrip

```python
>>> a = " hi "
>>> a.rstrip()
' hi'
```

### 양쪽 공백 지우기 - strip

```python
>>> a = " hi "
>>> a.strip()
'hi'
```

### 문자열 바꾸기 - replace

```python
>>> a = "Life is too short"
>>> a.replace("Life", "Your leg")
'Your leg is too short'
```

### 문자열 나누기 - split

```python
>>> a = "Life is too short"
>>> a.split()   # 공백을 기준으로 문자열 나눔
['Life', 'is', 'too', 'short']
>>> b = "a:b:c:d"
>>> b.split(':')  # :를 기준으로 문자열 나눔
```
