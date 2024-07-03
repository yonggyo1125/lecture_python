# 사용자 입출력

## 사용자 입력 활용하기

> 사용자가 입력한 값을 어떤 변수에 대입하고 싶을 때

### input 사용하기

```python
>>> a = input()
Life is too short, you need python
>>> a
'Life is too short, you need python'
```

- input은 사용자가 키보드로 입력한 모든 것을 문자열로 저장한다.

### 프롬프트를 띄워 사용자 입력받기

> input()의 괄호 안에 안내 문구를 입력하여 프롬프트를 띄워 주면 된다.

```python
input("안내_문구")
```

```python
>>> number = input("숫자를 입력하세요: ")
숫자를 입력하세요:
```
- ‘숫자를 입력하세요’라는 프롬프트에 3을 입력하면 변수 number에 값 3이 대입된다. 

```python
>>> number = input("숫자를 입력하세요: ")
숫자를 입력하세요: 3
>>> print(number)
3
```

- input은 입력되는 모든 것을 문자열로 취급하기 때문에 number는 숫자가 아닌 문자열이라는 것에 주의

```python
>>> type(number)
<class 'str'>
```

## print 자세히 알기

> print 문의 용도는 데이터를 출력하는 것

```python
>>> a = 123
>>> print(a)
123
>>> a = "Python"
>>> print(a)
Python
>>> a = [1, 2, 3]
>>> print(a)
[1, 2, 3]
```

### 큰따옴표로 둘러싸인 문자열은 + 연산과 동일하다

```python
>>> print("life" "is" "too short")  # 1번
lifeistoo short
>>> print("life"+"is"+"too short")  # 2번
lifeistoo short
```
- 따옴표로 둘러싸인 문자열을 연속해서 쓰면 + 연산을 한 것과 같다.

## 문자열 띄어쓰기는 쉼표로 한다

```python
>>> print("life", "is", "too short")
life is too short
```

## 한 줄에 결괏값 출력하기

- 한 줄에 결괏값을 계속 이어서 출력하려면 매개변수 end를 사용해 끝 문자를 지정해야 한다.

```python
>>> for i in range(10):
...     print(i, end=' ')
...
0 1 2 3 4 5 6 7 8 9 >>>
```

- end 매개변수의 초깃값은 줄바꿈(\n) 문자이다.