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
