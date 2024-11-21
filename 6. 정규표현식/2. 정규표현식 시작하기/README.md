# 정규 표현식 시작하기
- 정규 표현식에서는 메타 문자(meta characters)를 사용한다. 먼저 메타 문자가 무엇인지 알아보자.

## 정규 표현식의 기초, 메타 문자
- 메타 문자란 원래 그 문자가 가진 뜻이 아니라 특별한 의미를 가진 문자를 말한다. 
- 정규 표현식에 다음과 같은 메타 문자를 사용하면 특별한 의미를 갖게 된다.

```python
. ^ $ * + ? { } [ ] \ | ( )
```

### \[ \] 문자 - 문자 클래스

- 우리가 가장 먼저 살펴볼 메타 문자는 바로 문자 클래스(character class)인 \[\]이다. 문자 클래스로 만들어진 정규식은 ‘\[’ 와 ‘\]’ 사이의 문자들과 매치’라는 의미를 갖는다.
- 문자 클래스를 만드는 메타 문자인 \[ \] 사이에는 어떤 문자도 들어갈 수 있다.
- 즉, 정규 표현식이 <code>\[abc\]</code>라면 이 표현식의 의미는 ‘a, b, c 중 한 개의 문자와 매치’를 뜻한다. 이해를 돕기 위해 문자열 "a", "before", "dude"가 정규식 <code>\[abc\]</code>와 어떻게 매치되는지 살펴보자.
    - "a"는 정규식과 일치하는 문자인 "a"가 있으므로 매치된다.
    - "before"는 정규식과 일치하는 문자인 "b"가 있으므로 매치된다.
    - "dude"는 정규식과 일치하는 문자인 a, b, c 중 어느 하나도 포함하고 있지 않으므로 매치되지 않는다.
- \[\] 안의 두 문자 사이에 하이픈(-)을 사용하면 두 문자 사이의 범위를 의미한다. 예를 들어 <code>\[a-c\]</code>라는 정규 표현식은 <code>\[abc\]</code>와 동일하고 <code>\[0-5\]</code>는 <code>\[012345\]</code>와 동일하다.
- 다음은 하이픈(-)을 사용한 문자 클래스의 사용 예이다.
    - \[a-zA-Z\] : 모든 알파벳
    - \[0-9\] : 모든 숫자
- 문자 클래스(\[\]) 안에는 어떤 문자나 메타 문자도 사용할 수 있지만, 주의해야 할 메타 문자가 1가지 있다. 그것은 바로 <code>^</code>인데, 문자 클래스 안에 ^ 메타 문자를 사용할 경우에는 반대(not)라는 의미를 갖는다. 예를 들어 <code>\[^0-9\]</code>라는 정규 표현식은 숫자가 아닌 문자만 매치된다.

### 자주 사용하는 문자 클래스

- <code>\[0-9\]</code> 또는 <code>\[a-zA-Z\]</code> 등은 무척 자주 사용하는 정규 표현식이다. 이렇게 자주 사용하는 정규식은 별도의 표기법으로 표현할 수 있다. 다음을 기억해 두자.
- <code>\d</code> - 숫자와 매치된다. <code>\[0-9\]</code>와 동일한 표현식이다.
- <code>\D</code> - 숫자가 아닌 것과 매치된다. <code>\[^0-9\]</code>와 동일한 표현식이다.
- <code>\s</code> - 화이트스페이스(whitespace) 문자와 매치된다. <code>\[\t\n\r\f\v\]</code>와 동일한 표현식이다. 맨 앞의 빈칸은 공백 문자(space)를 의미한다.
- <code>\S</code> - 화이트스페이스 문자가 아닌 것과 매치된다. <code>\[^ \t\n\r\f\v\]</code>와 동일한 표현식이다.
- <code>\w</code> - 문자+숫자(alphanumeric)와 매치된다. <code>\[a-zA-Z0-9_\]</code>와 동일한 표현식이다.
- <code>\W</code> - 문자+숫자(alphanumeric)가 아닌 문자와 매치된다. <code>\[^a-zA-Z0-9_\]</code>와 동일한 표현식이다.
- 대문자로 사용된 것은 소문자의 반대임을 추측할 수 있다.

### .(dot) 문자 - <code>\n</code>을 제외한 모든 문자

- 정규 표현식의 .(dot) 메타 문자는 줄바꿈 문자인 <code>\n</code>을 제외한 모든 문자와 매치된다는 것을 의미한다.

> 정규식을 작성할 때 <code>re.DOTALL</code> 옵션을 주면 .(dot) 문자와 <code>\n</code> 문자도 매치된다.

- 다음 정규식을 살펴보자.

```
a.b
```

- 위 정규식의 의미는 다음과 같다.

```
"a + 모든_문자 + b"
```

- 즉, a와 b라는 문자 사이에 어떤 문자가 들어가도 모두 매치된다는 의미이다.
- 이해를 돕기 위해 문자열 "aab", "a0b", "abc"가 정규식 <code>a.b</code>와 어떻게 매치되는지 살펴보자.
    - "aab"는 가운데 문자 "a"가 모든 문자를 의미하는 <code>.</code>과 일치하므로 정규식과 매치된다.
    - "a0b"는 가운데 문자 "0"가 모든 문자를 의미하는 <code>.</code>과 일치하므로 정규식과 매치된다.
    - "abc"는 "a"문자와 "b"문자 사이에 어떤 문자라도 하나는 있어야 하는 이 정규식과 일치하지 않으므로 매치되지 않는다.
- 앞의 식과 조금 다른 다음 정규식을 살펴보자.

```
a[.]b
```

- 이렇게 \[\] 안에 <code>.</code> 문자를 쓰면 여기서 <code>.</code>는 메타 문자가 아니라 ‘.’ 문자 그대로를 의미한다. 즉, 이 정규식의 의미는 다음과 같다.

```
"a + . + b"
```

- 따라서 정규식 <code>a\[.\]b</code>는 "a.b" 문자열과 매치되고 "a0b" 문자열과는 매치되지 않는다. 혼동하지 않도록 주의하자.

### <code>*</code> 문자

```
ca*t
```

- 이 정규식은 반복을 의미하는 <code>*</code> 메타 문자를 사용했다. 여기에서 사용한 <code>*</code>은 <code>*</code> 바로 앞에 있는 문자 a가 0부터 무한대까지 반복될 수 있다는 의미이다.

> <code>*</code> 메타 문자의 반복 개수가 무한대라고 표현했는데, 메모리 용량에 한계가 있어 실제로는 약 2억 개라고 한다.

- 즉, 다음과 같은 문자열이 모두 매치된다.

|정규식|문자열|매치 여부|설명|
|---|---|---|----|
|<code>ca*t</code>|ct|Yes|"a"가 0번 반복되어 매치|
|<code>ca*t</code>|cat|Yes|"a"가 0번 이상 반복되어 매치(1번 반복)|
|<code>ca*t</code>|caaat|Yes|"a"가 0번 이상 반복되어 매치(3번 반복)|


### + 문자

- 반복을 나타내는 또 다른 메타 문자로 <code>+</code>가 있다. <code>+</code>는 최소 1번 이상 반복될 때 사용한다. 즉, <code>*</code>가 반복 횟수가 0부터라면 <code>+</code>는 반복 횟수가 1부터인 것이다.

- 다음 정규식을 살펴보자.

```
ca+t
```

- 위 정규식의 의미는 다음과 같다.

```
"c + a가_1번_이상_반복 + t"
```

- 위 정규식에 대한 매치 여부는 다음 표와 같다.

|정규식|문자열|매치 여부|설명|
|---|---|---|----|
|<code>ca+t</code>|ct|No|"a"가 0번 반복되어 매치되지 않음|
|<code>ca+t</code>|cat|Yes|"a"가 1번 이상 반복되어 매치 (1번 반복)|
|<code>ca+t</code>|caaat|Yes|"a"가 1번 이상 반복되어 매치 (3번 반복)|

### {} 문자와 ? 문자

- {m, n} 정규식을 사용하면 반복 횟수가 m부터 n까지인 문자와 매치할 수 있다. m 또는 n을 생략할 수도 있다. 만약 {3,}처럼 사용하면 반복 횟수가 3 이상인 경우이고 {,3}처럼 사용하면 반복 횟수가 3 이하인 경우를 의미한다. 생략된 m은 0과 동일하며, 생략된 n은 무한대(약 2억 개 미만)의 의미를 갖는다.
- <code>{1,}</code>은 <code>+</code>, <code>{0,}</code>은 <code>*</code>와 동일하다.

#### {m}

```
ca{2}t
```

- 이 정규식의 의미는 다음과 같다.

```
"c + a를_반드시_2번_반복 + t"
```

- 이 정규식에 대한 매치 여부는 다음 표와 같다.

|정규식|문자열|매치 여부|설명|
|---|---|---|-----|
|<code>ca{2}t</code>|cat|No|"a"가 1번만 반복되어 매치되지 않음.|
|<code>ca{2}t</code>|caat|Yes|"a"가 2번 반복되어 매치|

#### {m, n}

```
ca{2,5}t
```

- 이 정규식의 의미는 다음과 같다.

```
"c + a를_2~5회_반복 + t"
```

- 이 정규식에 대한 매치 여부는 다음 표와 같다.

|정규식|문자열|매치 여부| 설명                  |
|---|---|---|---------------------|
|<code>ca{2,5}t</code>|cat|No|"a"가 1번만 반복되어 매치되지 않음|
|<code>ca{2,5}t</code>|caat|Yes|"a"가 2번 반복되어 매치|
|<code>ca{2,5}t</code>|Yes|"a"가 5번 반복되어 매치|

#### <code>?</code>
- <code>?</code> 메타 문자가 의미하는 것은 <code>{0, 1}</code>이다.
- 다음 정규식을 살펴보자.

```
ab?c
```

- 이 정규식의 의미는 다음과 같다.

```
"a + b가_있어도_되고_없어도_됨 + c"
```

- 이 정규식에 대한 매치 여부는 다음 표와 같다.

|정규식|문자열|매치 여부|설명|
|---|---|----|-----|
|<code>ab?c</code>|abc|Yes|"b"가 1번 사용되어 매치|
|<code>ab?c</code>|ac|Yes|"b"가 0번 사용되어 매치|

- 즉, b 문자가 있거나 없거나 둘 다 매치되는 경우이다.
- <code>*</code>, <code>+</code>, <code>?</code> 메타 문자는 모두 <code>{m, n}</code> 형태로 고쳐 쓰는 것이 가능하지만, 이해하기 쉽고 표현도 간결한 <code>*</code>, <code>+</code>, <code>?</code> 메타 문자를 사용하는 것이 좋다.
- 지금까지 매우 기초적인 정규 표현식에 대해 알아보았다. 알아야 할 것들이 아직 많이 남아 있지만, 그에 앞서 파이썬으로 정규 표현식을 어떻게 사용할 수 있는지 알아보자.

## 파이썬에서 정규 표현식을 지원하는 re 모듈

- 파이썬은 정규 표현식을 지원하기 위해 re(regular expression) 모듈을 제공한다. re 모듈은 파이썬을 설치할 때 자동으로 설치되는 표준 라이브러리로, 사용 방법은 다음과 같다.

```python
>>> import re
>>> p = re.compile('ab*')
```

- re.compile을 사용하여 정규 표현식(위 예에서는 <code>ab*</code>)을 컴파일한다. re.compile의 리턴값을 객체 p(컴파일된 패턴 객체)에 할당해 그 이후의 작업을 수행할 것이다.
  - 정규식을 컴파일할 때 특정 옵션을 주는 것도 가능한데, 이에 대해서는 뒤에서 자세히 살펴본다.
  - 턴이란 정규식을 컴파일한 결과이다.

## 정규식을 이용한 문자열 검색

- 이제 컴파일된 패턴 객체를 사용하여 문자열 검색을 수행해 보자. 컴파일된 패턴 객체는 다음과 같은 4가지 메서드를 제공한다.

|Method|목적|
|----|-----|
|match()|문자열의 처음부터 정규식과 매치되는지 조사한다.|
|search()|문자열 전체를 검색하여 정규식과 매치되는지 조사한다.|
|findall()|정규식과 매치되는 모든 문자열(substring)을 리스트로 리턴한다.|
|finditer()|정규식과 매치되는 모든 문자열(substring)을 반복 가능한 객체로 리턴한다.|

- match, search는 정규식과 매치될 때는 match 객체를 리턴하고 매치되지 않을 때는 None을 리턴한다. match 객체란 정규식의 검색 결과로 리턴된 객체를 말한다.
- 먼저 다음과 같은 패턴을 만들어 보자.

```python
>>> import re
>>> p = re.compile('[a-z]+')
```

- 이제 이 패턴 객체로 앞에 나온 메서드를 사용하는 간단한 예를 살펴보자.

### match

- match 메서드는 문자열의 처음부터 정규식과 매치되는지 조사한다. 앞 패턴에 match 메서드를 수행해 보자.

```python
>>> m = p.match("python")
>>> print(m)
<re.Match object; span=(0, 6), match='python'>
```
- "python" 문자열은 <code>\[a-z\]+</code> 정규식에 부합되므로 match 객체가 리턴된다.

```python
>>> m = p.match("3 python")
>>> print(m)
None
```

- "3 python" 문자열은 처음에 나오는 문자 3이 정규식 <code>\[a-z\]+</code>에 부합되지 않으므로 None이 리턴된다.
- match의 결과로 match 객체 또는 None을 리턴하기 때문에 파이썬 정규식 프로그램은 보통 다음과 같은 흐름으로 작성한다.

```python
p = re.compile(정규표현식)
m = p.match('조사할 문자열')
if m:
    print('Match found: ', m.group())
else:
    print('No match')
```

- 즉, match의 결괏값이 있을 때만 그다음 작업을 수행하겠다는 것이다.


### search

- 컴파일된 패턴 객체 p를 가지고 이번에는 search 메서드를 수행해 보자.

```python
>>> m = p.search("python")
>>> print(m)
<re.Match object; span=(0, 6), match='python'>
```

- "python" 문자열에 search 메서드를 수행하면 match 메서드를 수행했을 때와 동일하게 매치된다.

```python
>>> m = p.search("3 python")
>>> print(m)
<re.Match object; span=(2, 8), match='python'>
```

- "3 python" 문자열의 첫 번째 문자는 "3"이지만, search는 문자열의 처음부터 검색하는 것이 아니라 문자열 전체를 검색하기 때문에 "3" 이후의 "python" 문자열과 매치된다.
- 이렇듯 match 메서드와 search 메서드는 문자열의 처음부터 검색할지의 여부에 따라 다르게 사용해야 한다.

### findall

- 이번에는 findall 메서드를 수행해 보자.

```python
>>> result = p.findall("life is too short")
>>> print(result)
['life', 'is', 'too', 'short']
```

- findall은 패턴(<code>\[a-z\]+</code>)과 매치되는 모든 값을 찾아 리스트로 리턴한다.

### finditer

- 이번에는 finditer 메서드를 수행해 보자.

```python
>>> result = p.finditer("life is too short")
>>> print(result)
<callable_iterator object at 0x01F5E390>
>>> for r in result: print(r)
...
<re.Match object; span=(0, 4), match='life'>
<re.Match object; span=(5, 7), match='is'>
<re.Match object; span=(8, 11), match='too'>
<re.Match object; span=(12, 17), match='short'>
```

- finditer는 findall과 동일하지만, 그 결과로 반복 가능한 객체(iterator object)를 리턴한다. 그리고 반복 가능한 객체가 포함하는 각각의 요소는 match 객체이다.

## match 객체의 메서드

- match 객체란 앞에서 살펴본 p.match, p.search 또는 p.finditer 메서드에 의해 리턴된 매치 객체(Match Object)를 의미한다. 이제 이 match 객체에 대해서 자세히 알아보자.
- 앞에서 정규식을 사용한 문자열 검색을 수행하면서 아마도 다음과 같은 궁금증이 생겼을 것이다.
  - 어떤 문자열이 매치되었는가?
  - 매치된 문자열의 인덱스는 어디서부터 어디까지인가?
- match 객체의 메서드를 사용하면 이 같은 궁금증을 해결할 수 있다. 다음 표를 살펴보자.

|method|목적|
|---|----|
|group|매치된 문자열을 리턴한다.|
|start|매치된 문자열의 시작 위치를 리턴한다.|
|end|매치된 문자열의 끝 위치를 리턴한다.|
|span|매치된 문자열의 (시작, 끝)에 해당하는 튜플을 리턴한다.|

- 다음 예로 확인해 보자.

```python
>>> m = p.match("python")
>>> m.group()
'python'
>>> m.start()
0
>>> m.end()
6
>>> m.span()
(0, 6)
```

- 예상한 대로 결괏값이 출력되는 것을 확인할 수 있다. match 메서드를 수행한 결과로 리턴된 match 객체로 start 메서드를 사용했을 때 결괏값은 항상 0일 수밖에 없다. match 메서드는 항상 문자열의 시작부터 조사하기 때문이다.
- 만약 search 메서드를 사용했다면 <code>m.start()</code> 값은 다음과 같이 다르게 나올 것이다.

```python
>>> m = p.search("3 python")
>>> m.group()
'python'
>>> m.start()
2
>>> m.end()
8
>>> m.span()
(2, 8)
```

### 모듈 단위로 수행하기

- 지금까지 우리는 re.compile을 사용하여 컴파일된 패턴 객체로 그 이후의 작업을 수행했다. re 모듈은 이를 더 축약한 형태로 사용할 수 있는 방법을 제공한다. 다음 예를 살펴보자

```python
>>> p = re.compile('[a-z]+')
>>> m = p.match("python")
```

- 이 코드가 축약된 형태는 다음과 같다.

```python
>>> m = re.match('[a-z]+', "python")
```

- 이렇게 사용하면 컴파일과 match 메서드를 한 번에 수행할 수 있다. 보통 한 번 만든 패턴 객체를 여러 번 사용해야 할 때는 이 방법보다 re.compile을 사용하는 것이 편리하다.

## 컴파일 옵션
- 정규식을 컴파일할 때 다음 옵션을 사용할 수 있다.
  - DOTALL(S) - .(dot)이 줄바꿈 문자를 포함해 모든 문자와 매치될 수 있게 한다.
  - IGNORECASE(I) - 대소문자에 관계없이 매치될 수 있게 한다.
  - MULTILINE(M) - 여러 줄과 매치될 수 있게 한다. <code>^</code>, <code>$</code> 메타 문자 사용과 관계 있는 옵션이다.
  - VERBOSE(X) - verbose 모드를 사용할 수 있게 한다. 정규식을 보기 편하게 만들 수 있고 주석 등을 사용할 수 있게 된다.
- 옵션을 사용할 때는 <code>re.DOTALL</code>처럼 전체 옵션 이름을 써도 되고 <code>re.S</code>처럼 약어를 써도 된다.

### DOTALL, S

- <code>.</code> 메타 문자는 줄바꿈 문자(<code>\n</code>)를 제외한 모든 문자와 매치되는 규칙이 있다. 만약 <code>\n</code> 문자도 포함하여 매치하고 싶다면 <code>re.DOTALL</code> 또는 <code>re.S</code> 옵션을 사용해 정규식을 컴파일하면 된다.
- 다음 예를 보자.

```python
>>> import re
>>> p = re.compile('a.b')
>>> m = p.match('a\nb')
>>> print(m)
None
```

- 정규식이 <code>a.b</code>인 경우 문자열 <code>a\\nb</code>는 매치되지 않는다는 것을 알 수 있다. <code>\n</code>은 <code>.</code> 메타 문자와 매치되지 않기 때문이다. <code>\\n</code> 문자와도 매치되게 하려면 다음과 같이 <code>re.DOTALL</code> 옵션을 사용해야 한다.

```python
>>> p = re.compile('a.b', re.DOTALL)
>>> m = p.match('a\nb')
>>> print(m)
<re.Match object; span=(0, 3), match='a\nb'>
```

- 보통 <code>re.DOTALL</code> 옵션은 여러 줄로 이루어진 문자열에서 줄바꿈 문자에 상관없이 검색할 때 많이 사용한다.

### IGNORECASE, I

- <code>re.IGNORECASE</code> 또는 <code>re.I</code> 옵션은 대소문자 구별 없이 매치를 수행할 때 사용하는 옵션이다. 다음 예제를 살펴보자.

```python
>>> p = re.compile('[a-z]+', re.I)
>>> p.match('python')
<re.Match object; span=(0, 6), match='python'>
>>> p.match('Python')
<re.Match object; span=(0, 6), match='Python'>
>>> p.match('PYTHON')
<re.Match object; span=(0, 6), match='PYTHON'>
```

- <code>\[a-z\]+</code> 정규식은 소문자만을 의미하지만, <code>re.I</code> 옵션으로 대소문자 구별 없이 매치된다.

### MULTILINE, M

- <code>re.MULTILINE</code> 또는 <code>re.M</code> 옵션은 조금 후에 설명할 메타 문자인 <code>^</code>, <code>$</code>와 연관된 옵션이다. 이 메타 문자에 대해 간단히 설명하면 <code>^</code>는 문자열의 처음, <code>$</code>는 문자열의 마지막을 의미한다. 예를 들어 정규식이 <code>^python</code>인 경우, 문자열의 처음은 항상 python으로 시작해야 매치되고 만약 정규식이 <code>python$</code>이라면 문자열의 마지막은 항상 python으로 끝나야 매치된다는 의미이다.
- 다음 예를 살펴보자.

```python
# multiline.py
import re
p = re.compile("^python\s\w+")

data = """python one
life is too short
python two
you need python
python three"""
```

- 정규식 <code>^python\s\w+</code>은 python이라는 문자열로 시작하고 그 뒤에 화이트스페이스, 그 뒤에 단어가 와야 한다는 의미이다.
- 이 스크립트를 실행하면 다음과 같은 결과를 리턴한다.

```python
['python one']
```

- <code>^</code> 메타 문자에 의해 python이라는 문자열을 사용한 첫 번째 줄만 매치된 것이다.
- 하지만 <code>^</code> 메타 문자를 문자열 전체의 처음이 아니라 각 라인의 처음으로 인식시키고 싶은 경우도 있을 것이다. 이럴 때 사용할 수 있는 옵션이 바로 <code>re.MULTILINE</code> 또는 <code>re.M</code>이다. 앞 코드를 다음과 같이 수정해 보자.

```python
# multiline.py
import re
p = re.compile("^python\s\w+", re.MULTILINE)

data = """python one
life is too short
python two
you need python
python three"""

print(p.findall(data))
```

- <code>re.MULTILINE</code> 옵션으로 인해 <code>^</code> 메타 문자가 문자열 전체가 아닌 각 줄의 처음이라는 의미를 가지게 되었다. 이 스크립트를 실행하면 다음과 같은 결과가 출력된다.

```
['python one', 'python two', 'python three']
```

- 즉, <code>re.MULTILINE</code> 옵션은 <code>^</code>, <code>$</code> 메타 문자를 문자열의 각 줄마다 적용해 주는 것이다.

### VERBOSE, X

- 지금껏 알아본 정규식은 매우 간단하지만, 정규식 전문가들이 만든 정규식을 보면 거의 암호 수준이다. 정규식을 이해하려면 하나하나 조심스럽게 뜯어 봐야만 한다. 이렇게 이해하기 어려운 정규식을 주석 또는 줄 단위로 구분할 수 있다면 얼마나 보기 좋고 이해하기 쉬울까? 이 경우에는 <code>re.VERBOSE</code> 또는 <code>re.X</code> 옵션을 사용하면 된다.
- 다음 예를 보자.

```python
charref = re.compile(r'&[#](0[0-7]+|[0-9]+|x[0-9a-fA-F]+);')
```

- 이 정규식이 쉽게 이해되는가? 이제 다음 예를 살펴보자.

```python
charref = re.compile(r"""
 &[#]                # Start of a numeric entity reference
 (
     0[0-7]+         # Octal form
   | [0-9]+          # Decimal form
   | x[0-9a-fA-F]+   # Hexadecimal form
 )
 ;                   # Trailing semicolon
""", re.VERBOSE)
```

- 첫 번째와 두 번째 예를 비교해 보면 컴파일된 패턴 객체인 charref는 모두 동일한 역할을 한다. 하지만 정규식이 복잡할 경우, 두 번째처럼 주석을 적고 여러 줄로 표현하는 것이 훨씬 가독성이 좋다는 것을 알 수 있다.
- <code>re.VERBOSE</code> 옵션을 사용하면 문자열에 사용된 화이트스페이스는 컴파일할 때 제거된다(단, \[ \] 안에 사용한 화이트스페이스는 제외).

## 역슬래시 문제

- 정규 표현식을 파이썬에서 사용할 때 혼란을 주는 요소가 1가지 있는데, 바로 역슬래시(<code>\</code>)이다.
- 예를 들어 어떤 파일 안에 있는 <code>"\section"</code> 문자열을 찾기 위한 정규식을 만든다고 가정해 보자.

```python
\section
```

- 이 정규식은 <code>\s</code> 문자가 whitespace로 해석되어 의도한 대로 매치가 이루어지지 않는다.
- 이 표현은 다음과 동일한 의미이다.

```
[ \t\n\r\f\v]ection
```

- 의도한 대로 매치하고 싶다면 다음과 같이 변경해야 한다.

```
\\section
```

- 즉, 앞 정규식에서 사용한 <code>\</code> 문자가 문자열 자체라는 것을 알려 주기 위해 역슬래시 2개를 사용해 이스케이프 처리를 해야 한다.
- 따라서 위 정규식을 컴파일하려면 다음과 같이 작성해야 한다.

```python
>>> p = re.compile('\\section')
```

- 그런데 여기에서 또 하나의 문제가 발견된다. 이처럼 정규식을 만들어서 컴파일하면 실제 파이썬 정규식 엔진에는 파이썬 문자열 리터럴 규칙에 따라 <code>\\</code>이 <code>\</code>로 변경되어 <code>\section</code>이 전달된다.

> 이 문제는 이와 같은 정규식을 파이썬에서 사용할 때만 발생한다(파이썬의 리터럴 규칙). 유닉스의 grep, vi 등에서는 이러한 문제가 없다.

- 결국 정규식 엔진에 <code>\\</code> 문자를 전달하려면 파이썬은 <code>\\\\</code>처럼 역슬래시를 4개나 사용해야 한다. 

> 정규식 엔진은 정규식을 해석하고 수행하는 모듈이다.

```python
>>> p = re.compile('\\\\section')
```

- 만약 이와 같이 <code>\</code>를 사용한 표현이 계속 반복되는 정규식이라면 너무 복잡해서 이해하기 어려울 것이다. 이 문제를 해결하려면 raw string 표현법을 사용해야 한다. 그 방법은 다음과 같다.

```python
>>> p = re.compile(r'\\section')
```

- 이와 같이 정규식 문자열 앞에 r 문자를 삽입하면 이 정규식은 raw string 규칙에 의해 역슬래시 2개 대신 1개만 써도 2개를 쓴 것과 동일한 의미를 가지게 된다.
