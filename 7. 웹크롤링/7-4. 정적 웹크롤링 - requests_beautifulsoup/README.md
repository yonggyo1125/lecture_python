# 정적 웹크롤링 - request / beautifulsoup

- 정적 웹 크롤링은 아주 간단합니다.
    - 1단계. 원하는 웹 페이지의 html문서를 싹 긁어온다.
    - 2단계. 긁어온 html 문서를 파싱(Parsing)한다.
    - 3단계. 파싱한 html 문서에서 원하는 것을 골라서 사용한다.
- 위의 3단계를 수행하기 위해 사용되는 패키지를 하나씩 살펴보겠습니다.

## 정적 웹크롤링 관련 패키지
### 1단계. requests
- html 문서를 가져올 때 사용하는 패키지입니다. requests는 사용자 친화적인 문법을 사용하여 다루기 쉬우면서 안정성이 뛰어나다고 합니다.
- 그래서 파이썬 기본 라이브러리에 포함된 urllib 패키지보다 자주 사용됩니다.

#### 설치 방법
- VS code의 터미널창에서 아래와 같이 입력하면 됩니다.
- 만약 anaconda를 사용하신다면 pip 대신 conda를 입력해주셔도 됩니다.

```python
pip install requests
```

#### 사용 방법

```python
# requests 패키지 가져오기
import requests               

# 가져올 url 문자열로 입력
url = 'https://www.naver.com'  

# requests의 get함수를 이용해 해당 url로 부터 html이 담긴 자료를 받아옴
response = requests.get(url)    

# 우리가 얻고자 하는 html 문서가 여기에 담기게 됨
html_text = response.text
```

### 2단계. BeautifulSoup4
- BeautifulSoup4 패키지는 매우 길고 정신없는 html 문서를 잘 정리되고 다루기 쉬운 형태로 만들어 원하는 것만 쏙쏙 가져올 때 사용합니다.
- 이 작업을 파싱(Parsing)이라고도 부릅니다.

![image](https://wikidocs.net/images/page/137915/%ED%8C%8C%EC%8B%B1_%EC%A0%84%ED%9B%84_%EC%9D%B4%EB%AF%B8%EC%A7%80.PNG)

#### 설치 방법
- 마찬가지로 VS code의 터미널창에서 아래와 같이 입력하면 됩니다.

```python
pip install beautifulsoup4
```

#### 사용 방법
- 방금 전 Requests 패키지로 받아온 html 문서를 파싱해야하므로, 이전 코드 블록을 실행하셔야 합니다.

```python
# BeautifulSoup 패키지 불러오기
# 주로 bs로 이름을 간단히 만들어서 사용함
from bs4 import BeautifulSoup as bs

# html을 잘 정리된 형태로 변환
html = bs(html_text, 'html.parser')
```


### 3단계. BeautifulSoup4 (find /select)

- 이제 마지막 3단계입니다.
- 사실 1, 2단계는 느끼셨겠지만 url만 수정하면 아주 쉽게 응용할 수 있을 정도로 쉽습니다.
- 즉, 정적 웹크롤링의 핵심은 필요한 정보의 위치와 구조를 파악해서 쏙쏙 가져오는 3단계입니다.
- 크롤링을 원하는 사이트가 생겼을 때에 능수능란하게 코딩하기 위해서는 꼭 이 스킬을 확실히 익혀두셔야 합니다.

#### find( ), find_all( ) 함수

- BeautifulSoup 패키지에서 find 함수는 아래와 같이 12개가 있습니다.
- 하지만 우리가 알면 되는 것은 딱 2개입니다. - find( ): 하나만 찾는 것 - find_all( ): 모두 다 찾는 것
- 주의할 것은 find로 찾는 것이 여러개라면 가장 첫 번째 것만 가져온다는 것입니다.

![image](https://wikidocs.net/images/page/137915/find_%ED%95%A8%EC%88%98_%EC%A2%85%EB%A5%98.PNG)

> 괄호( ) 안에는 html의 태그(tag)나 속성(attribute)이 들어갑니다. 웹 크롤링 관련 코드를 보다보면 find 함수를 종종 사용한 경우를 보는데, 그 코드를 이해할 목적으로만 가볍게 알고 넘어가시는 것을 추천 드립니다. 왜냐하면 CSS 선택자 개념을 사용하는 select( ) 함수를 사용하는 것이 훨씬 직관적이거든요!

```python
# 목표 태그 예)
<p class = "para">코딩유치원</p>
<div id = "zara">코딩유치원</p>

# 태그 이름으로 찾기
soup.find('p')

# 태그 속성(class)으로 찾기 - 2가지 형식
soup.find(class_='para') #이 형식을 사용할 때는 class 다음에 언더바_를 꼭 붙여주어야 한다
soup.find(attrs = {'class':'para'}) 

# 태그 속성(id)으로 찾기 - 2가지 형식
soup.find(id='zara') 
soup.find(attrs = {'id':'zara'})

# 태그 이름과 속성으로 찾기
soup.find('p', class_='para')
soup.find('div', {'id' = 'zara'})
```

#### select( ), select_one( ) 함수

- select( )는 find_all( )과 같은 개념이고, select_one( )은 find( )와 같은 개념입니다. 다만, select( ) 함수는 괄호( )안에 CSS 선택자라는 것을 넣어서 원하는 정보를 찾는 것이 특징입니다.
- 아주 직관적이고 쉬워서 이 방법을 추천드립니다

```python
# a태그의 class 속성명이 news_tit인 태그 
soup.select_one('a.news_tit')

soup.select('a.news_tit')

for i in titles: 
    title = i.get_text() print(title)
```