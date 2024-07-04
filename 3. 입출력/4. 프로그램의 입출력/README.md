# 프로그램의 입출력

## sys 모듈 사용하기

- 파이썬에서는 sys 모듈을 사용하여 프로그램에 인수를 전달할 수 있다. 
- sys 모듈을 사용하려면 다음 예의 import sys처럼 import 명령어를 사용해야 한다.

```python
# sys1.py 
import sys

args = sys.argv[1:]
for i in args:
    print(i)
```

- sys 모듈의 argv는 프로그램 실행 시 전달된 인수를 의미한다. 
- argv\[0\]은 파일 이름 sys1.py가 되고 argv\[1\]부터는 뒤에 따라오는 인수가 차례대로 argv의 요소가 된다.
- 이 프로그램을 C:\doit 디렉터리에 저장한 후 인수를 전달하여 실행하면 다음과 같은 결과를 볼 수 있다.

```
C:\doit>python sys1.py aaa bbb ccc
aaa
bbb
ccc
```

- 위 예를 응용하여 다음과 같은 간단한 프로그램을 만들어 보

```python
# sys2.py
import sys
args = sys.argv[1:]
for i in args:
    print(i.upper(), end=' ')
```

- 문자열 관련 함수인 upper()를 사용하여 프로그램 실행 시 전달된 인수를 모두 대문자로 바꾸어 주는 간단한 프로그램이다. 
- 명령 프롬프트 창에서 다음과 같이 실행해 보자.

```
C:\doit>python sys2.py life is too short, you need python
```

- 출력 결과

```
LIFE IS TOO SHORT, YOU NEED PYTHON
```