# 웹크롤링

##  웹 크롤링이란 ?
- 웹 크롤링(또는 스크래핑)은 웹 페이지에서 자동으로 정보를 추출하는 프로세스를 의미합니다.
- 데이터 수집, 연구 수행 또는 주가 확인, 웹 페이지 변경 추적과 같은 다양한 반복 작업을 자동화하는데 자주 사용되고 있습니다.
- 크롤링하는 웹 페이지의 서비스 약관을 준수해야 함 / 짧은 시간 내 서버에 많은 요청을 전송하여 부하를 과도하게 주는 행위는 서버에 무리를 줄 수 있음

## requests 및 BeautifulSoup

### reqeusts
- requests 는 HTTP 요청을 쉽게 보낼 수 있도록 하는 파이썬 HTTP requests 라이브러리입니다.

### BeautifulSoup(bs4)

- BeautifulSoup 은 HTML 및 XML 문서의 구문을 분석하는 라이브러리입니다.
- 두 라이브러리를 결합하면 요청으로 웹 페이지를 가져온 후 BeautifulSoup을 사용하여 특정 컨텐츠 구문을 분석하고, 추출할 수 있습니다.

### 모듈 설치

- 웹 크롤링을 진행하기 전 앞에서 본 라이브러리를 사용하기 위해 pip 를 이용하여 두 라이브러리를 설치해야 합니다.
- 아래 명령어를 사용하여 모듈을 설치합니다.

```python
pip install requests bs4
```

### 기본 웹 크롤링 예제

- 간단한 웹 크롤링 예제에 대해 알아보도록 하겠습니다.
- '보안뉴스' 에서 기사들의 제목을 가져오는 간단한 실습을 진행하도록 하겠습니다.


```python
import requests
from bs4 import BeautifulSoup

url = 'http://www.boannews.com/media/t_list.asp'
response = requests.get(url)  # GET 메소드를 사용하여 url에 HTTP Request 전송

if response.status_code == 200:  # 정상 응답 반환 시 아래 코드블록 실행
    soup = BeautifulSoup(response.content, 'html.parser')  # 응답 받은 HTML 파싱
    titles = soup.select('div.news_list')  # 파싱한 데이터에서 div 태그 내 news_list 클래스 내 데이터 저장

    for title in titles:
        print(title.select_one('span.news_txt').get_text())  # news_txt 클래스의 텍스트 데이터 출력

else:
    print('error')  # 오류 시 메시지 출력
```

### `find( )` 및 `find_all( )` 메소드 사용

- BeautifulSoup 은 HTML 요소를 찾는 여러가지 방법을 제공하는데 그 중 두 가지를 살펴보도록 하겠습니다.

#### `find( )` 메소드

- 첫 번째로 일치하는 태그를 반환합니다.

```python
h1_tag = soup.find('h1')
print(f"H1 Tag: {h1_tag}')
```

- 위와 같은 코드를 작성하여 실행할 경우 파싱된 데이터에서 h1 태그를 찾는데 그 중 첫 번째 요소를 h1_tag 에 저장하고 출력하게 된다.

#### `find_all( )` 메소드

- 일치하는 모든 태그를 리스트 형태로 반환합니다.

```python
p_tags = soup.find_all('p')
for index, p in enumerate(p_tags, 1):
	print(f"{index}: {p.text}')
```

- 위와 같은 코드를 작성하여 실행할 경우 파싱된 데이터에서 p 태그를 모두 찾아 p_tags에 리스트 형태로 저장한 후 for 구문을 통해 하나씩 출력하는 형태의 코드이다.

### 속성으로 검색하기

- 속성을 기준으로 태그를 지정하여 검색할 수 있습니다.
- `find( )` 메소드를 사용한 데이터 추출 시 해당 태그로 지정된 다양한 요소가 있는 경우 id 등 유니크 값을 추가로 지정하여 원하는 데이터를 추출할 수 있습니다.

```python
specific_tag = soup.find('div', id='<id>') # div 태그 요소 중 지정된 id 값의 요소를 추출
print(specific_tag)
```

### CSS Selector 를 이용한 데이터 추출

- BeautifulSoup 은 `select( )` 메소드를 사용한 CSS Selector도 지원합니다.


#### CSS Class 를 기반으로 데이터 추출

```python
# BeautifulSoup를 사용하여 .classname 클래스의 모든 요소를 선택합니다
class_elements = soup.select('.classname')

# 각 요소의 텍스트를 출력합니다
for element in class_elements:
    print(element.text)
```

#### ID 를 기반으로 데이터 추출

```python
id_element = soup.select_one('#element_id') # 지정된 ID 요소의 값 하나만 id_element에 저장
print(id_element.text)
```