# 딕셔너리 자료형
- 사람은 누구든지 "이름" = "홍길동", "생일" = "몇 월 며칠" 등과 같은 방식으로 그 사람이 가진 정보를 나타낼 수 있다. 
- 이러한 대응 관계를 나타낼 수 있는 자료형이 딕셔너리(dictionary) 이다.
- 이를 딕셔너리라고 하고, ‘연관 배열(associative array)’또는 ‘해시(hash)’라고도 한다.

## 딕셔너리란?

- 딕셔너리는 Key와 Value를 한 쌍으로 가지는 자료형이다. 
- 리스트나 튜플처럼 순차적으로(sequential) 해당 요솟값을 구하지 않고 Key를 통해 Value를 얻는다.


## 딕셔너리는 어떻게 만들까?

- 다음은 딕셔너리의 기본 모습이다.

```python
{Key1: Value1, Key2: Value2, Key3: Value3, ...}
```

- Key와 Value의 쌍 여러 개가 {}로 둘러싸여 있다. 
- 각각의 요소는 Key: Value 형태로 이루어져 있고 쉼표(,)로 구분되어 있다.

```python
>>> dic = {'name': 'pey', 'phone': '010-9999-1234', 'birth': '1118'}
```

-  Key는 각각 'name', 'phone', 'birth', 각각의 Key에 해당하는 Value는 'pey', '010-9999-1234', '1118'이 된다.


|key|value|
|---|----|
|name|pey|
|phone|010-9999-1234|
|birth|1118|

- Key로 정숫값 1, Value로 문자열 'hi'를 사용한 예

```python
>>> a = {1: 'hi'}
```

- Value에 리스트도 넣을 수 있습니다.

```python
>>> a = {'a': [1, 2, 3]}
```

## 딕셔너리 쌍 추가, 삭제하기

### 딕셔너리 쌍 추가하기

```python
>>> a = {1: 'a'}
>>> a[2] = 'b'
>>> a
{1: 'a', 2: 'b'}
```

- {1: 'a'} 딕셔너리에 a\[2\] = 'b'와 같이 입력하면 딕셔너리 a에 Key와 Value가 각각 2와 'b'인 {2: 'b'} 딕셔너리 쌍이 추가된다.

```python
>>> a['name'] = 'pey';
>>> a
{1: 'a', 2: 'b', 'name': 'pey'}
```

- 딕셔너리 a에 {'name': 'pey'} 쌍이 추가되었다.

```python
>>> a[3] = [1, 2, 3]
>> a
{1: 'a', 2: 'b', 'name': 'pey', 3: [1, 2, 3]}
```

- Key는 3, Value는 \[1, 2, 3\]을 가지는 한 쌍이 또 추가되었다.

### 딕셔너리 요소 삭제하기

```python
>>> del a[1]
>>> a
{2: 'b', 'name': 'pey', 3: [1, 2, 3]}
```

- del 함수를 사용해서 del a\[key\]를 입력하면 지정한 Key에 해당하는 {Key: Value} 쌍이 삭제된다.

## 딕셔너리를 사용하는 방법

### 딕셔너리에서 Key를 사용해 Value 얻기

```python
>>> grade = {'pey': 10, 'julliet': 99}
>>> grade['pey']
10
>>> grade['julliet']
99
```

- 'pey'라는 Key의 Value를 얻기 위해 grade\['pey'\]를 사용한 것처럼 어떤 Key의 Value를 얻기 위해서는 '딕셔너리_변수_이름\[Key\]'를 사용해야 한다.

```python
>>> a = {1: 'a', 2: 'b'}
>>> a[1]
'a'
>>> a[2]
'b'
```

- 딕셔너리는 리스트나 튜플에 있는 인덱싱 방법을 적용할 수 없다. 
- a\[1\]은 딕셔너리 {1: 'a', 2: 'b'}에서 Key가 1인 것의 Value인 'a'를 리턴한다. a\[2\] 역시 마찬가지이다.
- a라는 변수에 앞의 예에서 사용한 딕셔너리의 Key와 Value를 뒤집어 놓은 딕셔너리를 대입해 보자.

```python
>>> a = {'a': 1, 'b': 2}
>>> a['a']
1
>>> a['b']
2
```

- a\['a'\], a\['b'\]처럼 Key를 사용해서 Value를 얻을 수 있다.

```python
>>> dic = {'name':'pey', 'phone':'010-9999-1234', 'birth': '1118'}
>>> dic['name']
'pey'
>>> dic['phone']
'010-9999-1234'
>>> dic['birth']
'1118'
```

### 딕셔너리 만들 때 주의할 사항

- 딕셔너리에서 Key는 고유한 값이므로 중복되는 Key 값을 설정해 놓으면 하나를 제외한 나머지 것들이 모두 무시된다.
- 다음 예에서 볼 수 있듯이 동일한 Key가 2개 존재할 경우, 1: 'a' 쌍이 무시된다.

```python
>>> a = {1:'a', 1:'b'}
>>> a
{1: 'b'}
```

- 딕셔너리에는 동일한 Key가 중복으로 존재할 수 없다.
- Key에 리스트는 쓸 수 없다는 것,  하지만 튜플은 Key로 쓸 수 있다.
- 딕셔너리의 Key로 쓸 수 있느냐, 없느냐는 Key가 변하는(mutable) 값인지, 변하지 않는(immutable) 값인지에 달려 있다. 
- 리스트는 그 값이 변할 수 있기 때문에 Key로 쓸 수 없다. 
- 다음 예처럼 리스트를 Key로 설정하면 리스트를 키 값으로 사용할 수 없다는 오류가 발생

```python
>>> a = {[1,2] : 'hi'}
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

- Value에는 변하는 값이든, 변하지 않는 값이든 아무 값이나 넣을 수 있다.

## 딕셔너리 관련 함수

### Key 리스트 만들기 - keys

```python
>>> a = {'name': 'pey', 'phone': '010-9999-1234', 'birth': '1118'}
>>> a.keys()
dict_keys(['name', 'phone', 'birth'])
```

- a.keys()는 딕셔너리 a의 Key만을 모아 dict_keys 객체를 리턴한다.
- dict_keys 객체는 다음과 같이 사용할 수 있다. 리스트를 사용하는 것과 별 차이는 없지만, 리스트 고유의 append, insert, pop, remove, sort 함수는 수행할 수 없다.

```python
>>> for k in a.keys():
...    print(k)
...
name
phone
birth
```

- dict_keys 객체를 리스트로 변환하려면 다음과 같이 하면 된다.

```python
>>> list(a.keys())
['name', 'phone', 'birth']
```

- Value 리스트 만들기 - values

```python
>>> a.values()
dict_values(['pey', '010-9999-1234', '1118'])
```

- Key, Value 쌍 얻기 - items

```python
>>> a.items()
dict_items([('name', 'pey'), ('phone', '010-9999-1234'), ('birth', '1118')])
```

- Key: Value 쌍 모두 지우기 - clear

```python
>>> a.clear()
>>> a
{}
```

- clear 함수는 딕셔너리 안의 모든 요소를 삭제한다.

### Key로 Value 얻기 - get

```python
>>> a = {'name': 'pey', 'phone': '010-9999-1234', 'birth': '1118'}
>>> a.get('name')
'pey'
>>> a.get('phone')
'010-9999-1234'
```

- get(x) 함수는 x라는 Key에 대응되는 Value를 리턴한다. 앞에서 살펴보았듯이 a.get('name')은 a\['name'\]을 사용했을 때와 동일한 결괏값을 리턴한다.
- a\['nokey'\]처럼 딕셔너리에 존재하지 않는 키로 값을 가져오려고 할 경우, a\['nokey'\] 방식은 오류를 발생시키고 a.get('nokey') 방식은 None을 리턴한다는 차이가 있다. 

```python
>>> a = {'name':'pey', 'phone':'010-9999-1234', 'birth': '1118'}
>>> print(a.get('nokey'))
None
>>> print(a['nokey’])
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
KeyError: 'nokey'
```

- 딕셔너리 안에 찾으려는 Key가 없을 경우, 미리 정해 둔 디폴트 값을 대신 가져오게 하고 싶을 때는 get(x, '디폴트 값')을 사용하면 편리하다.

```python
>>> a.get('nokey', 'foo')
'foo'
```

- 딕셔너리 a에는 'nokey'에 해당하는 Key가 없다. 따라서 디폴트 값인 'foo'를 리턴한다.

### 해당 Key가 딕셔너리 안에 있는지 조사하기 - in

```python
>>> a = {'name':'pey', 'phone':'010-9999-1234', 'birth': '1118'}
>>> 'name' in a
True
>>> 'email' in a
False
```