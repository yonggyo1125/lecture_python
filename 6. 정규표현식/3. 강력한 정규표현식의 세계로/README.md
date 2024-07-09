# 강력한 정규 표현식의 세계로

## 문자열 소비가 없는 메타 문자

- 여기에서 다룰 메타 문자는 앞에서 살펴본 메타 문자와 성격이 조금 다르다. 앞에서 살펴본 <code>+</code>, <code>*</code>, <code>\[\]</code>, <code>{}</code> 등의 메타 문자는 매치가 성사되면 문자열을 탐색하는 시작 위치가 변경된다(보통 소비된다고 표현한다). 
- 가령 <code>aac</code>라는 문자열에서 <code>a+</code>라는 패턴을 찾아야 할 때, <code>aa</code>가 매치되고 나면 문자열 중 <code>aa</code>는 소비되고 남은 <code>c</code>가 시작 위치가 된다.

### |
- <code>|</code> 메타 문자는 or과 동일한 의미로 사용된다. <code>A|B</code>라는 정규식이 있다면 A 또는 B라는 의미가 된다.

```python
>>> p = re.compile('Crow|Servo')
>>> m = p.match('CrowHJello')
>>> print(m)
<re.Match object; span=(0, 4), match='Crow'>
```


### ^

- <code>^</code> 메타 문자는 문자열의 맨 처음과 일치한다는 것을 의미한다. 앞에서 살펴본 컴파일 옵션 <code>re.MULTILINE</code>을 사용할 경우에는 여러 줄의 문자열일 때 각 줄의 처음과 일치하게 된다.

```python
>>> print(re.search('^Life', 'Life is too short'))
<re.Match object; span=(0, 4), match='Life'>
>>> print(re.search('^Life', 'My Life'))
None
```
- <code>^Life</code> 정규식은 Life 문자열이 처음에 온 경우에는 매치하지만, 처음 위치가 아닌 경우에는 매치되지 않는다는 것을 알 수 있다.

### $

- <code>$</code> 메타 문자는 <code>^</code> 메타 문자와 반대의 경우이다. 즉, <code>$</code>는 문자열의 끝과 매치한다는 것을 의미한다.

- 다음 예를 살펴보자.

```python
>>> print(re.search('short$', 'Life is too short'))
<re.Match object; span=(12, 17), match='short'>
>>> print(re.search('short$', 'Life is too short, you need python'))
None
```

- <code>short$</code> 정규식은 검색할 문자열이 short로 끝난 경우에는 매치되지만, 이외의 경우에는 매치되지 않는다는 것을 알 수 있다.
- <code>^</code> 또는 <code>$</code> 문자를 메타 문자가 아닌 문자 그 자체로 매치하고 싶은 경우에는 <code>\^</code>, <code>\$</code>로 작성하면 된다.

### \A

- <code>\A</code>는 문자열의 처음과 매치된다는 것을 의미한다. <code>^</code> 메타 문자와 동일한 의미이지만, <code>re.MULTILINE</code> 옵션을 사용할 경우에는 다르게 해석된다. 
- <code>re.MULTILINE</code> 옵션을 사용할 경우 <code>^</code>은 각 줄의 문자열의 처음과 매치되지만, <code>\A</code>는 줄과 상관없이 전체 문자열의 처음하고만 매치된다.

### \Z

- <code>\Z</code>는 문자열의 끝과 매치된다는 것을 의미한다.
- 이것 역시 <code>\A</code>와 동일하게 <code>re.MULTILINE</code> 옵션을 사용할 경우, <code>$</code> 메타 문자와는 달리 전체 문자열의 끝과 매치된다.

### \b

- <code>\b</code>는 단어 구분자(word boundary)이다. 보통 단어는 화이트스페이스에 의해 구분된다.
- 다음 예를 살펴보자.

```python
>>> p = re.compile(r'\bclass\b')
>>> print(p.search('no class at all'))
<re.Match object; span=(3, 8), match='class'>
```

- <code>\bclass\b</code> 정규식은 앞뒤가 화이트스페이스로 구분된 class라는 단어와 매치된다는 것을 의미한다. 따라서 no class at all의 class라는 단어와 매치된다는 것을 확인할 수 있다.

```python
>>> print(p.search('the declassified algorithm'))
```
- 앞 예의 the declassified algorithm 문자열 안에도 class 문자열이 포함되어 있기는 하지만, whitespace로 구분된 단어가 아니므로 매치되지 않는다.

```python
>>> print(p.search('one subclass is'))
None
```

- subclass 문자열 역시 class 앞에 sub 문자열이 더해져 있으므로 매치되지 않는다는 것을 알 수 있다.
- <code>\b</code> 메타 문자를 사용할 때 주의해야 할 점이 있다. 
- <code>\b</code>는 파이썬 리터럴 규칙에 따르면 백스페이스(backspace)를 의미하므로 백스페이스가 아닌 단어 구분자라는 것을 알려 주기 위해 <code>r'\bclass \b'</code>처럼 raw string이라는 것을 알려 주는 r을 반드시 붙여야 한다.

### \B

- <code>\B</code> 메타 문자는 <code>\b</code> 메타 문자와 반대의 경우이다. 즉, 화이트스페이스로 구분된 단어가 아닌 경우에만 매치된다.

```python
>>> p = re.compile(r'\Bclass\B')
>>> print(p.search('no class at all'))  
None
>>> print(p.search('the declassified algorithm'))
<re.Match object; span=(6, 11), match='class'>
>>> print(p.search('one subclass is'))
None
```

- class 단어의 앞뒤에 화이트스페이스가 하나라도 있는 경우에는 매치가 되지 않는다는 것을 확인할 수 있다.

## 그루핑
- ABC 문자열이 계속해서 반복되는지 조사하는 정규식을 작성하고 싶다고 가정해 보자. 이때 필요한 것이 바로 그루핑(grouping)이다.
- 앞에서 말한 정규식은 다음처럼 그루핑을 사용하면 작성할 수 있다.

```
(ABC)+
```

- 그룹을 만들어 주는 메타 문자는 바로 <code>()</code>이다.

```python
>>> p = re.compile('(ABC)+')
>>> m = p.search('ABCABCABC OK?')
>>> print(m)
<re.Match object; span=(0, 9), match='ABCABCABC'>
>>> print(m.group())
ABCABCABC
```

- 다음 예를 살펴보자.

```python
>>> p = re.compile(r"\w+\s+\d+[-]\d+[-]\d+")
>>> m = p.search("park 010-1234-1234")
```
- <code>\w+\s+\d+\[-\]\d+\[-\]\d+은 이름 + " " + 전화번호</code> 형태의 문자열을 찾는 정규식이다. 그런데 이렇게 매치된 문자열 중에서 이름만 뽑아 내고 싶다면?

> 보통 반복되는 문자열을 찾을 때 그룹을 사용하는데, 그룹을 사용하는 더 중요한 이유는 매치된 문자열 중에서 특정 부분의 문자열만 뽑아 내기 위해서이다.

- 앞 예에서 만약 "이름" 부분만 뽑아 내려 한다면 다음과 같이 할 수 있다.

```python
>>> p = re.compile(r"(\w+)\s+\d+[-]\d+[-]\d+")
>>> m = p.search("park 010-1234-1234")
>>> print(m.group(1))
park
```

- 이름에 해당하는 <code>\w+</code> 부분을 <code>(\w+)</code>과 같이 그룹으로 만들면 match 객체의 group(인덱스) 메서드를 사용하여 그루핑된 부분의 문자열만 뽑아 낼 수 있다. group 메서드의 인덱스는 다음과 같은 의미를 가진다.

|group(인덱스)|설명|
|---|-----|
|group(0)|매치된 전체 문자열|
|group(1)|첫 번째 그룹에 해당하는 문자열|
|group(2)|두 번째 그룹에 해당하는 문자열|
|group(n)|n 번째 그룹에 해당하는 문자열|

- 다음 예제를 계속해서 살펴보자.

```python
>>> p = re.compile(r"(\w+)\s+(\d+[-]\d+[-]\d+)")
>>> m = p.search("park 010-1234-1234")
>>> print(m.group(2))
010-1234-1234
```

- 이번에는 전화번호 부분을 그룹 <code>(\d+\[-\]\d+\[-\]\d+)</code>로 만들었다. 이러면 <code>group(2)</code>처럼 사용해 전화번호만 뽑아 낼 수 있다.
- 만약 전화번호 중에서 국번만 뽑아 내고 싶으면 어떻게 해야 할까? 다음과 같이 국번 부분을 또 그루핑하면 된다.

```python
>>> p = re.compile(r"(\w+)\s+((\d+)[-]\d+[-]\d+)")
>>> m = p.search("park 010-1234-1234")
>>> print(m.group(3))
010
```

- <code>(\w+)\s+((\d+)\[-\]\d+\[-\]\d+)</code>처럼 그룹을 중첩해 사용할 수도 있다. 그룹이 중첩된 경우는 바깥쪽부터 시작해 안쪽으로 들어갈수록 인덱스 값이 증가한다.

### 그루핑된 문자열 재참조하기

- 그룹의 또 하나 좋은 점은 한 번 그루핑한 문자열을 재참조(backreferences)할 수 있다는 점이다. 다음 예를 살펴보자.

```python
>>> p = re.compile(r'(\b\w+)\s+\1')
>>> p.search("Paris in the the spring").group()
'the the'
```

- 정규식 (\b\w+)\s+\1은 (그룹) + " " + 그룹과 동일한 단어와 매치된다는 것을 의미한다. 이렇게 정규식을 만들면 2개의 동일한 단어를 연속적으로 사용해야만 매치된다. 
