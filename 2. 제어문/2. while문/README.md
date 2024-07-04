# while문

## while 문의 기본 구조

```python
while 조건문:
    수행할_문장1
    수행할_문장2
    수행할_문장3
    ...
```

- while 문은 조건문이 참인 동안 while 문에 속한 문장들이 반복해서 수행된다.
- ‘열 번 찍어 안 넘어가는 나무 없다’라는 속담을 파이썬 프로그램으로 만들면 다음과 같다.

```python
>>> treeHit = 0
>>> while treeHit < 10:
...     treeHit = treeHit +1
...     print("나무를 %d번 찍었습니다." % treeHit)
...     if treeHit == 10:
...         print("나무 넘어갑니다.")
...
나무를 1번 찍었습니다.
나무를 2번 찍었습니다.
나무를 3번 찍었습니다.
나무를 4번 찍었습니다.
나무를 5번 찍었습니다.
나무를 6번 찍었습니다.
나무를 7번 찍었습니다.
나무를 8번 찍었습니다.
나무를 9번 찍었습니다.
나무를 10번 찍었습니다.
나무 넘어갑니다.
```

> treeHit = treeHit + 1은 프로그래밍을 할 때 매우 자주 사용하는 기법이다. treeHit 값을 1만큼씩 증가시킬 목적으로 사용하며 treeHit += 1처럼 작성해도 된다.

## while 문 만들기
- 여러 가지 선택지 중 하나를 선택해서 입력받는 예제

```python
>>> prompt = """
... 1. Add
... 2. Del
... 3. List
... 4. Quit
...
... Enter number: """
>>>
```

- number 변수에 0을 먼저 대입한다. 이렇게 변수를 먼저 설정해 놓지 않으면 다음에 나올 while 문의 조건문인 number != 4에서 변수가 존재하지 않는다는 오류가 발생한다.

```python
>>> number = 0
>>> while number != 4:
...     print(prompt)
...     number = int(input())
...

1. Add
2. Del
3. List
4. Quit

Enter number:
```

- while 문을 보면 number가 4가 아닌 동안 prompt를 출력하고 사용자로부터 번호를 입력받는다. 다음 결과 화면처럼 사용자가 값 4를 입력하지 않으면 계속해서 prompt를 출력
- input()으로 입력 받은 값은 문자이므로 int()와 같은 함수를 사용하여 숫자로 변환한다. <code>number = int(input())</code>

```python
Enter number:
1

1. Add
2. Del
3. List
4. Quit
```

- 4를 입력하면 조건문이 거짓이 되어 while 문을 빠져나가게 된다.

```python
Enter number:
4
>>>
```

## while 문 강제로 빠져나가기
- while 문은 조건문이 참인 동안 계속 while 문 안의 내용을 반복적으로 수행한다. 하지만 강제로 while 문을 빠져나가고 싶을 때가 있다.
- 이떄는 break문을 사용하면 된다.

- 커피 자판기 이야기를 파이썬 프로그램으로 표현해 본 예

```python
>>> coffee = 10
>>> money = 300
>>> while money:
...     print("돈을 받았으니 커피를 줍니다.")
...     coffee = coffee -1
...     print("남은 커피의 양은 %d개입니다." % coffee)
...     if coffee == 0:
...         print("커피가 다 떨어졌습니다. 판매를 중지합니다.")
...         break
...
```

- money가 300으로 고정되어 있고 while money:에서 조건문인 money는 0이 아니기 때문에 항상 참이다. 따라서 무한히 반복되는 무한 루프를 돌게 된다.
- 그리고 while 문의 내용을 한 번 수행할 때마다 coffee = coffee - 1에 의해 coffee의 개수가 1개씩 줄어든다.
- 만약 coffee가 0이 되면 if coffee == 0: 문장에서 coffee == 0이 참이 되므로 if 문 다음 문장 "커피가 다 떨어졌습니다. 판매를 중지합니다."가 출력되고 break 문이 호출되어 while 문을 빠져나가게 된다.
- 다음은 자판기의 실제 작동 과정과 비슷하게 만들어 본 예
- IDLE 에디터를 사용해서 작성해 보자.

```python
# coffee.py
coffee = 10
while True:
    money = int(input("돈을 넣어 주세요: "))
    if money == 300:
        print("커피를 줍니다.")
        coffee = coffee -1
    elif money > 300:
        print("거스름돈 %d를 주고 커피를 줍니다." % (money -300))
        coffee = coffee -1
    else:
        print("돈을 다시 돌려주고 커피를 주지 않습니다.")
        print("남은 커피의 양은 %d개 입니다." % coffee)
    if coffee == 0:
        print("커피가 다 떨어졌습니다. 판매를 중지 합니다.")
        break
```

```python
money = int(input("돈을 넣어 주세요: "))
```

> 이 문장은 사용자로부터 값을 입력받는 부분이고 입력받은 숫자를 money 변수에 대입하는 것

- coffee.py 파일을 저장한 후 명령 프롬프트 창을 열어 프로그램을 직접 실행해 보자.

```python
python coffee.py
돈을 넣어 주세요:
```

- 입력란에 여러 숫자를 입력해 보면서 결과를 확인하자

```python
돈을 넣어 주세요: 500
거스름돈 200를 주고 커피를 줍니다.
돈을 넣어 주세요: 300
커피를 줍니다.
돈을 넣어 주세요: 100
돈을 다시 돌려주고 커피를 주지 않습니다.
남은 커피의 양은 8개입니다.
돈을 넣어 주세요:
```

## while 문의 맨 처음으로 돌아가기

- 프로그래밍을 하다 보면 while 문을 빠져나가지 않고 while 문의 맨 처음(조건문)으로 다시 돌아가게 만들고 싶은 경우가 생기게 된다. 
- 이때 사용하는 것이 바로 continue 문이다.
- 1부터 10까지의 숫자 중에서 홀수만 출력하는 것을 while 문을 사용해서 작성하는 예

```python
>>> a = 0
>>> while a < 10:
...     a = a + 1
...     if a % 2 == 0: continue
...     print(a)
...
1
3
5
7
9
```

## 무한 루프
- 무한 루프란 무한히 반복한다는 의미
- 파이썬에서 무한 루프는 while 문으로 구현할 수 있다.
- 다음은 무한 루프의 기본 형태이다.

```python
while True: 
    수행할_문장1 
    수행할_문장2
    ...
```
- while 문의 조건문이 True이므로 항상 참이 된다. 따라서 while 문 안에 있는 문장들은 무한히 수행될 것이다.
- 무한 루프의 예

```python
>>> while True:
...     print("Ctrl+C를 눌러야 while문을 빠져나갈 수 있습니다.")
...
Ctrl+C를 눌러야 while문을 빠져나갈 수 있습니다.
Ctrl+C를 눌러야 while문을 빠져나갈 수 있습니다.
Ctrl+C를 눌러야 while문을 빠져나갈 수 있습니다.
....
```