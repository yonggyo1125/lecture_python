# 연결 리스트(Linked List)

> 연결 리스트는 데이터를 연속된 메모리 공간에 저장하지 않고, 각 데이터가 다음 데이터의 위치를 가리키는 방식으로 구성된 선형 자료 구조다. 각 데이터 단위를 노드라고 하며, 노드는 데이터를 저장하고 다음 노드를 가리키는 참조(주소)를 포함한다.
>
> 배열은 인덱스를 사용해 원소에 쉽게 접근할 수 있지만, 원소를 추가하거나 삭제하려면 연속된 메모리 공간을 확보하고 원소들을 이동시켜야 하므로 시간이 걸린다. 반면, 자료의 양이 정해져 있지 않거나 추가 및 삭제가 빈번할 때는 연결 리스트가 더 적합하다.

## 단일 연결 리스트(Singly Linked List)의 구조

- 각 노드는 값과 다음 노드의 주소(참조)를 저장한다.
- head는 연결 리스트의 첫 번째 노드를 가리키며, 연결 리스트에 접근하기 위한 시작점 역할을 한다.

![image](https://wikidocs.net/images/page/224937/fig-015_.png)

## 연결 리스트의 특징

- **동적 크기**: 배열과 달리 크기가 고정되어 있지 않아, 필요에 따라 노드를 추가하거나 삭제하며 크기를 조절할 수 있다.
- **삽입과 삭제가 쉬움**: 배열에서는 삽입/삭제 시 해당 위치 이후의 모든 요소를 이동시켜야 하지만, 연결 리스트에서는 링크만 변경하면 되므로 효율적이다.
- **메모리 효율성**: 배열은 미리 메모리 공간을 할당해야 하지만, 연결 리스트는 필요한 만큼만 메모리를 할당하므로 메모리 낭비를 줄일 수 있다.

## 파이썬에서의 구현

> 파이썬에서는 모든 것이 객체이며, 변수는 객체를 참조하는 역할을 한다. 따라서 연결 리스트를 객체 지향 방식으로 쉽게 구현할 수 있다.

![image](https://wikidocs.net/images/page/224937/fig-016_.png)

- 먼저, 각 노드를 표현하는 Node 클래스를 정의한다.

```python
class Node:
    def __init__(self, data):
        self.data = data  #data는 값을 가리키는 변수(속성, attribute)
        self.next = None  #next는 다음 노드를 가리키는 변수
```

## 간단한 연결 리스트 만들기

### 노드를 생성하고 연결하기

- 파이썬에서 연결 리스트를 만들 때는, 첫 번째 노드에 head라는 참조를 붙여서 시작한다. 연결 리스트를 만드는 과정은 다음과 같다.

  - 첫째 노드를 만들고 head라는 이름표를 붙인다. (head에 첫째 노드를 할당)
  - 둘째 노드를 만들고, head의 next가 둘째 노드를 가리키도록 한다.
    - 셋째 노드를 만들고, head의 next의 next가 셋째 노드를 가리키도록 한다.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

head = Node(1)
head.next = Node(2)
head.next.next = Node(3)
```

- 아래 그림은 마지막까지 실행했을 때의 상태다. 위에서 그린 연결 리스트의 모양과 같다.

![image](https://wikidocs.net/images/page/224937/fig-018.png)

## 연결 리스트의 값을 출력하기

- 위 그림을 보면 각 노드의 값을 순서대로 출력하는 것은 어렵지 않다

![image](https://wikidocs.net/images/page/224937/fig-019_.png)

- head부터 마지막 노드까지 이동하면서 data를 출력한다.
- 이때 head는 연결 리스트의 시작이므로, head가 이동하면 연결 리스트를 잃게 된다.
- 따라서 변수(이름표)를 만들고 head부터 마지막 노드까지 이동하면서 data를 출력한다.
- 마지막 노드의 next는 None을 가리키므로, 노드가 None이 아닐 동안 계속 이동하면서 data를 출력한다.

- 위 코드에 이어서 아래 코드를 입력하고 실행한다.

```python
node = head
while node:
    print(node.data, end = " ")
    node = node.next
```

```
1 2 3
```

## 연결 리스트의 끝에 새 노드를 추가하기

> 연결 리스트의 끝에 노드를 추가하기 위해 `head.next...next = Node(data)` 처럼 코드를 쓰는 것은 불편하다. 연결 리스트의 값을 순서대로 출력하는 코드를 응용하여, 끝에 새 노드를 추가하자.

- 변수를 만들고 head부터 마지막 노드까지 이동한다.
- 마지막 노드의 next가 새 노드를 가리키도록 한다. (next에 새 노드를 할당)

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

head = Node(1)
head.next = Node(2)
head.next.next = Node(3)

node = head
while node.next: # 현재 노드의 next가 None이 아닐 동안 실행
    node = node.next
node.next = Node(4)
```

![image](https://wikidocs.net/images/page/224937/fig-020.png)

## 연결 리스트의 처음에 새 노드를 추가하기

- 첫 노드인 head 앞에 노드를 추가할 때, 연결 리스트의 연결이 끊어지지 않도록 아래 그림처럼 세 단계로 나눠서 노드를 추가한다.

![image](https://wikidocs.net/images/page/224937/fig-021_.png)

- 1 추가할 노드를 생성한다.
- 2 추가할 노드의 next가 head를 가리키게 한다.
- 3 head를 추가한 노드로 옮긴다.

> 위의 규칙에 따라 위에서 만든 연결 리스트의 첫 노드 앞에 0을 추가해 보자.

```python
node = Node(0)
node.next = head
head = node
```

- (1)과 (2) 과정을 실행했을 때의 상태는 아래와 같다.

![image](https://wikidocs.net/images/page/224937/fig-022.png)

- 최종 상태는 아래 그림과 같다.

![image](https://wikidocs.net/images/page/224937/fig-023.png)

- 이처럼 연결 리스트는 노드 간의 참조만 변경하여 노드를 추가하거나 삭제할 수 있는 효율적인 자료 구조다. 이를 활용하면 동적으로 변하는 데이터를 효율적으로 관리할 수 있다.

# 연결 리스트 클래스를 만들고, 노드 추가하기

- 앞서 간단하게 연결 리스트를 만들어서, 노드를 처음과 끝에 추가하고 출력하는 방법을 살펴봤다. 노드를 검색하거나 꺼내는 것(pop)도 생각보다 어렵지 않아 보인다. 단일 연결 리스트 클래스를 만들고, 관련 메서드를 하나씩 만들어 보자.
- 구현할 단일 연결 리스트의 메서드는 아래와 같다. 이름은 리스트와 데크(deque)의 메서드 이름을 참조했다.

  - **appendleft(x)**: 연결 리스트의 처음에 x를 추가한다.
  - **append(x)**: 연결 리스트의 끝 x를 추가한다.
  - **popleft()**: 연결 리스트에서 첫 노드의 값을 반환하고, 노드는 삭제한다.
  - **pop()**: 연결 리스트에서 마지막 노드의 값을 반환하고, 노드는 삭제한다.
  - **insert(i, x)**: 연결 리스트의 i번 인덱스에 x를 추가한다.
  - **remove(x)**: 연결 리스트에서 값이 x인 노드를 찾아 삭제한다.
  - **reverse()**: 연결 리스트를 제자리에서 순서를 뒤집는다.

- 위의 메서드 외에 연결 리스트를 출력하고, 길이를 반환하고, 값을 검색하는 메서드도 만든다. 이들은 클래스의 특수 메소드로 구현한다.
  - **\_\_len\_\_**: len() 함수를 사용할 때 연결 리스트의 길이를 반환한다.
  - **\_\_contains\_\_**: 연산자 in과 not in을 사용할 때 연결 리스트 내의 값을 검사하여 True, False를 반환한다.
  - **\_\_str\_\_**: str()과 print() 함수를 사용할 때 출력할 문자열을 반환한다.

## 연결 리스트 클래스 만들기

> 앞서 만든 노드 클래스는 그대로 사용하다. 연결 리스트 클래스의 초기화 메서드에서는 연결 리스트에 접근하기 위해 필요한 head 속성과 연결 리스트의 길이를 저장할 length 속성을 초기화 한다

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
        self.length = 0

    def __len__(self):
        return self.lenth
```

## appendleft() 메서드 만들기

![image](https://wikidocs.net/images/page/224937/fig-021_.png)

> 위 그림은 이미 연결 리스트에 노드가 있을 때, 즉 `head`가 `None` 이 아닐 때 노드를 연결 리스트의 처음에 추가하는 과정을 나타낸 것이다. 따라서 앞서 만든 코드에 `head`를 검사하여 `None`이면 생성한 노드를 `head`에 할당하는 코드만 추가하면 된다.

- head가 None이면 생성한 노드를 head에 할당한다.
- head가 None이 아니면
  - 1 노드를 생성한다.
  - 2 노드의 next에 head를 할당한다.
  - 3 head를 새로 만든 노드로 옮긴다.
- 연결 리스트의 길이를 증가시킨다.

```python
class Node:
    ...

class LinkedList:
    def __init__(self):
        ...

    def __len__(self):
        ...

    def appendleft(self, data):
        if self.head is None:
            self.head = Node(data)
        else:
            node = Node(data)
            node.next = self.head
            self.head = node
        self.length += 1

if __name__ == "__main__":
    my_list = LinkedList()
    print(f"연결 리스트 생성.  연결 리스트의 길이 = {len(my_list)}")
    print()
    for i in range(4):
        my_list.appendleft(i)
        print(f"{i}을(를) 추가.  연결 리스트의 길이 = {len(my_list)}")
```

- 실행 결과

```
연결 리스트 생성.  연결 리스트의 길이 = 0

0을(를) 추가.  연결 리스트의 길이 = 1
1을(를) 추가.  연결 리스트의 길이 = 2
2을(를) 추가.  연결 리스트의 길이 = 3
3을(를) 추가.  연결 리스트의 길이 = 4
```

- 0을 추가했을 때

![image](https://wikidocs.net/images/page/225002/fig-024.png)

- 3까지 모두 추가했을 때

![image)(https://wikidocs.net/images/page/225002/fig-025.png)

## append 메서드 만들기

![image](https://wikidocs.net/images/page/225002/fig-026.png)

- `head`가 `None`이면 생성한 노드를 `head`에 할당한다.
- `head`가 `None`이 아니면
  - (1) 임시 노드를 만들어 마지막 노드까지 이동한다.
  - (2) 새 노드를 만든다.
  - (3) 임시 노드의 `next`에 노드를 할당한다.
- 연결 리스트의 길이를 증가시킨다.
- 위의 과정대로 구현한 코드는 아래와 같습니다.

```python
class Node:
    def __init__(self, data):
        ...


class LinkedList:
    def __init__(self):
        ...

    def __len__(self):
        ...

    def appendleft(self, data):
        ...

    def append(self, data):
        if self.head is None:
            self.head = Node(data)
        else:
            node = self.head
            while node.next is not None:
                node = node.next
            node.next = Node(data)
        self.length += 1


if __name__ == "__main__":
    my_list = LinkedList()
    print(f"연결 리스트 생성.  연결 리스트의 길이 = {len(my_list)}")
    print()
    for i in range(4):
        my_list.append(i)
        print(f"{i}을(를) 추가.  연결 리스트의 길이 = {len(my_list)}")
```

- 실행 결과

```
연결 리스트 생성.  연결 리스트의 길이 = 0

0을(를) 추가.  연결 리스트의 길이 = 1
1을(를) 추가.  연결 리스트의 길이 = 2
2을(를) 추가.  연결 리스트의 길이 = 3
3을(를) 추가.  연결 리스트의 길이 = 4
```

- 오류없이 실행되지만, 그냥 결과만 봐서는 `appendleft()` 메서드와 차이점이 보이지 않는다. Python Tutor에서 실행한 결과를 보면 아래와 같다.

![image](https://wikidocs.net/images/page/225002/fig-027.png)

- 그림을 보면, `appendleft()`와 data의 순서가 반대인 것을 확인할 수 있다.

# 연결 리스트의 상태를 출력하고, 값을 검색하기

## 연결 리스트 상태 출력하기

- 간단한 연결 리스트 만들기에서는 임시 노드를 만들고 `head`부터 마지막 노드까지 이동하면 `print` 함수로 값을 출력했다. 여기서는 특수 메서드인 \_\_str\_\_를 구현하여 `print()`함수로 연결 리스트의 상태를 출력한다.

![image](https://wikidocs.net/images/page/224937/fig-019_.png)

- 연결 리스트의 상태를 나타낼 문자열 변수를 만든다.
- 임시 노드가 None이 아닐 동안 계속 이동하면서 아래 과정을 반복한다.
  - 현재 노드의 값을 문자열로 변환하여 문자열 변수에 더한다.
  - 임시 노드를 다음 노드로 옮긴다. -문자열을 반환한다.

### 코드

```python
class Node:
    def __init__(self, data):
        ...


class LinkedList:
    def __init__(self):
        ...

    def __len__(self):
        ...

    def appendleft(self, data):
        ...

    def append(self, data):
        ...

    def __str__(self):
        if self.head is None:
            return "Linked list is empty!"
        res = "Head"
        node = self.head
        while node is not None:
            res += " → " + str(node.data)
            node = node.next
        return res


if __name__ == "__main__":
    my_list = LinkedList()
    print(f"연결 리스트 생성.  연결 리스트의 길이 = {len(my_list)}")
    print(my_list)
    print()
    for i in range(4):
        if i % 2:
            my_list.append(i)
        else:
            my_list.appendleft(i)
        print(f"{i}을(를) 추가.  연결 리스트의 길이 = {len(my_list)}")
        print(my_list)
        print()
```

### 실행 결과

```
연결 리스트 생성.  연결 리스트의 길이 = 0
Linked list is empty!

0을(를) 추가.  연결 리스트의 길이 = 1
Head → 0

1을(를) 추가.  연결 리스트의 길이 = 2
Head → 0 → 1

2을(를) 추가.  연결 리스트의 길이 = 3
Head → 2 → 0 → 1

3을(를) 추가.  연결 리스트의 길이 = 4
Head → 2 → 0 → 1 → 3
```

### 값을 검색하기

- 값을 검색하는 것은 `\_\_str\_\_` 메서드에서 값을 출력하는 부분을 삭제하고, 값을 비교하여 찾는 값이 있으면 True를 반환하도록 수정한다. 물론 찾는 값이 없으면 False를 반환한다.

- `head`가 `None`이면 False를 반환한다.
- 임시 노드가 None이 아닐 동안 계속 이동하면서 아래 과정을 반복한다.
- 현재 노드의 값이 찾는 값이면 True를 반환한다.
- 임시 노드를 다음 노드로 옮긴다.
- False를 반환한다.

```python
class Node:
    def __init__(self, data):
        ...


class LinkedList:
    def __init__(self):
        ...

    def __len__(self):
        ...

    def appendleft(self, data):
        ...

    def append(self, data):
        ...

    def __str__(self):
        ...

    def __contains__(self, target):
        if self.head is None:
            return False
        node = self.head
        while node is not None:
            if node.data == target:
                return True
            node = node.next
        return False

if __name__ == "__main__":
    import random
    data = list(range(10, 20))
    random.shuffle(data)
    my_list = LinkedList()
    for i in data:
        my_list.append(i)
    print(f"연결 리스트의 상태\n{my_list}")
    print()
    for _ in range(4):
        i = random.randint(5, 25)
        if i in my_list:
            print(f"{i}는(은) 연결 리스트에 있습니다.")
        else:
            print(f"{i}는(은) 연결 리스트에 없습니다.")
```

### 실행 결과

```
연결 리스트의 상태
Head → 11 → 17 → 12 → 14 → 18 → 15 → 13 → 10 → 19 → 16

19는(은) 연결 리스트에 있습니다.
23는(은) 연결 리스트에 없습니다.
20는(은) 연결 리스트에 없습니다.
17는(은) 연결 리스트에 있습니다.
```
