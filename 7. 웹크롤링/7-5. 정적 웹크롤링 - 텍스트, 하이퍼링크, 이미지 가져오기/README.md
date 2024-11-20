# 정적 웹크롤링 - 텍스트, 하이퍼링크, 이미지 가져오기
- 지난 시간에 배웠듯이 정적 웹 크롤링은 아주 간단합니다.
    - 1단계. 원하는 웹 페이지의 html문서를 싹 긁어온다.
    - 2단계. 긁어온 html 문서를 파싱(Parsing)한다.
    - 3단계. 파싱한 html 문서에서 원하는 것을 골라서 사용한다.
- 오늘은 3단계, 원하는 것을 골라서 사용하는 방법을 조금 더 자세히 다루어 볼 예정입니다.

## 크롤링 할 페이지(url) HTML 가져오기
- 해당 코드는 1단계와 2단계에 해당하는 코드입니다. 자세한 내용은 코드의 주석을 참고해주세요.

```python
# step1.프로젝트에 필요한 패키지 불러오기

from bs4 import BeautifulSoup as bs

import requests


# step2. 검색할 키워드 입력

query = input('검색할 키워드를 입력하세요: ')


# step3. 입력받은 query가 포함된 url 주소(네이버 뉴스 검색 결과 페이지) 저장

url = 'https://search.naver.com/search.naver?where=news&sm=tab_jum&query='+'%s'%query


# step4. requests 패키지를 이용해 'url'의 html 문서 가져오기

response = requests.get(url)

html_text = response.text


# step5. beautifulsoup 패키지로 파싱 후, 'soup' 변수에 저장

soup = bs(response.text, 'html.parser')
```


## 크롤링 할 페이지 실제로 들어가서 추출할 HTML 확인하기
- 코드를 실행하시면 vs code의 터미널 창에 '검색할 키워드를 입력하세요: '라고 출력될텐데, 원하는 검색 키워드를 입력하시면 됩니다.
- 저의 경우엔 '추석'을 검색해보았습니다.

![image](https://wikidocs.net/images/page/142389/Sep-19-2021_16-11-24.gif)

- 검색을 하셨다면 F12를 눌러서 HTML 문서가 출력되도록 해주시고, 이제부터 원하는 부분을 추출해보도록 하겠습니다.

### 텍스트 추출 / .get_text()

- requests와 beautifulsoup를 이용한 텍스트 추출 방법은 아래와 같습니다.
- 1번. 우측 개발자 도구에서 커서 모양의 아이콘을 클릭 2번. 추출을 원하는 부분, 여기서는 뉴스 제목을 클릭 3번. 해당 부분의 HTML 태그를 분석하여 select() 함수로 추출

![image](https://wikidocs.net/images/page/142389/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-09-19_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_5.34.58.png)

- 3번 단계를 조금 더 자세히 설명드려보겠습니다.
- css selector, 여기서는 a.news_tit이 되겠네요. 이 선택자는 해당 페이지의 뉴스 기사 제목 10개가 공통으로 가지고 있는 class 이름입니다.
- css selector를 알아냈다면 select 함수에 입력하여 원하는 부분의 html을 변수에 저장해준 후에, for 문과 .get_text( ) 함수를 이용해 주시면 됩니다.

```python
#step6.뉴스 제목 텍스트 추출

news_titles = soup.select("a.news_tit")

for i in news_titles:
    title = i.get_text()
    print(title)
```

### 링크 추출 / .attrs\['href'\]

- 링크를 가져오고 싶을 때, 속성을 가져오는 .attrs\['href'\] 함수를 사용합니다. href 속성은 방금 전 가져온 news_titles 변수에 저장되어 있으므로, 따로 한 번더 가져와줄 필요 없이 바로 for문을 써줬습니다.

```python
#step7.뉴스 하이퍼링크 추출

for i in news_titles:
    href = i.attrs['href']
    print(href)

```

- 결과는 아래와 같이 10개의 url이 출력되는 것을 확인하실 수 있을거예요.

![image](https://wikidocs.net/images/page/142389/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-09-19_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_6.34.47.png)


### 이미지 추출 .attrs\['src'\]

- 다음으로는 이미지 추출입니다. 텍스트나 url 링크를 가져올 때와는 다르게 조금 길지만 어려워 하실 필요없어요.
- 앞서 배우신 것과 같이 이미지 주소(src)를 갖고 있는 html을 news_thumnail 변수에 저장해줍니다.
- 그 다음엔 이미지 다운로드를 위해서 해당 주소들을 리스트(link_thumnail)에 append 함수를 이용해 하나씩 담아주세요.
- 사진을 다운로드 받아서 내 PC에 저장하기 위해서는 저장할 폴더를 만들고, src 주소를 이용해 다운로드 해주면 됩니다.
- 폴더 생성에는 os 모듈과 urllib.request 패키지의 urlretrieve 함수가 필요한데, 모두 다 파이썬 내장 라이브러리이므로 따로 설치해주실 필요 없이 
- import 해주시면 돼요.

```python
#step8.뉴스 썸네일 이미지 추출

news_content_div = soup.select(".news_contents")

news_thumbnail = [thumbnail.select_one(".thumb") for thumbnail in news_content_div]

link_thumbnail = []

for img in news_thumbnail:
    if img is  not  None  and  'data-lazysrc'  in img.attrs:
        link_thumbnail.append(img.attrs['data-lazysrc'])

# 이미지 저장할 폴더 생성
import os

# path_folder의 경로는 각자 저장할 폴더의 경로를 적어줄 것(ex.img_download)
path_folder = 'D:/images/img_download/'

if not os.path.isdir(path_folder):
    os.mkdir(path_folder)

# 이미지 다운로드
from urllib.request import urlretrieve

i = 0

for link in link_thumbnail:          
    i += 1
    urlretrieve(link, path_folder + f'{i}.jpg')
```
