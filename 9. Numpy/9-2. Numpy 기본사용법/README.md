# Numpy 사용방법

> NumPy는 배열을 만드는 빠르고 효율적인 방법을 다양하게 제공한다. 그리고 그 내부의 수치 데이터를 조작하는것이 편리하다.

- **넘파이를 가져오는 방법**

```python
import numpy as np
```

- 코드의 가독성을 높이기 위해 가져온 이름을 다음과 같이 단축한다 넘파이. 이는 코드를 더 읽기 쉽게 만들기 위해 널리 채택된 규칙이라고 볼 수 있다.

## array

> numpy의 array는 동일한 타입으로만 이루어진다. 이는, numpy의 연산을 매우 빠르게 진행하기 위한 것이다. 여기서, numpy array는 여러가지 기본 array 생성 방법이 있다. 주로 쓰는 4가지 먼저 이야기하겠다. 배열은 NumPy 라이브러리의 중앙 데이터 구조라고 할 수 있다. 배열은 values 및 원시 데이터에 대한 정보, 요소를 찾는 방법, 요소를 해석하는 방법. 인덱싱할 수 있는 요소 그리드가 있다.

### array 만들기

```python
import numpy as np
range_array = np.arange(10)
print(range_array)
```

```
[0 1 2 3 4 5 6 7 8 9]
```

- 아래와 같이 일일이 입력해서 사용할 수 도 있다.

```python
import numpy as np
a = np.array([1, 2, 3, 4, 5])
print(a)

[1 2 3 4 5]
```

- range_array에는 0이상 10미만의 정수로 이루어진 array가 생성된다

### array의 추가, 삭제

- 축, 종류, 함수를 호출할 때 순서를 지정합니다. : `np.sort()`
- array 연결 및 합치기 : `np.concatenate`

```python
x = np.array([[1, 1], [2, 2]])
y = np.array([[5, 6]])
np.concatenate((x, y), axis=0)

array([[1, 1],
       [2, 2],
       [5, 6]])
```
