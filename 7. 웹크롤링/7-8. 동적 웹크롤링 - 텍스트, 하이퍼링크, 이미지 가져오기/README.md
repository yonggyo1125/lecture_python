# 동적 웹크롤링 - 텍스트, 하이퍼링크, 이미지 가져오기

- 이번 시간에는 Selenium 패키지를 이용한 동적 웹크롤링을 할 때, 텍스트와 속성(하이퍼링크, 이미지)을 가져오는 방법에 대해서 알아보겠습니다.
- 실습을 통해서 하나씩 알아볼텐데요. 대략적인 순서는 이렇습니다.
    - 검색할 키워드 입력
    - 크롬 드라이버로 원하는 url 접속
    - 뉴스 제목 텍스트 추출
    - 뉴스 url 링크 추출
    - 뉴스 썸네일 이미지 추출
        - 이미지 src 리스트에 저장
        - 이미지 저장할 폴더 생성
        - src를 이용해 이미지 다운로드
- 우선 지난 강의에서 배웠던 1번 2번 단계는 설명 없이 코드만 공유드리고 넘어가도록 하겠습니다.

```python
#step1.selenium 패키지와 time 모듈 import
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
import time

#step2.검색할 키워드 입력
query = input('검색할 키워드를 입력하세요: ')

#step3.크롬드라이버로 원하는 url로 접속
url = 'https://www.naver.com/'
driver = webdriver.Chrome('/Users/sangwoo/Desktop/chromedriver')
driver.get(url)
time.sleep(3)

#step4.검색창에 키워드 입력 후 엔터
search_box = driver.find_element(By.ID, "query")
search_box.send_keys(query)
search_box.send_keys(Keys.RETURN)
time.sleep(2)

#step5.뉴스 탭 클릭
driver.find_element_by_xpath('//*[@id="lnb"]/div[1]/div/ul/li[2]/a').click()
time.sleep(2)
```

- 참고로 위의 코드를 실행하면 아래와 같이 입력한 키워드의 뉴스 검색 결과가 출력됩니다. 참고로 한 페이지에 뉴스는 10개가 출력됩니다.

![image](https://blog.kakaocdn.net/dn/zL1Op/btq7SMmdX14/Pl89PvykH5226wvvVhuqRK/img.gif)

- 해당 화면이 출력되셨다면 F12 버튼을 누르시고 크롤링을 원하는 부분을 selenium 패키지로 가져와야합니다.
- 오늘 사용할 html은 아래의 빨간색 사각형으로 표시한 부분입니다. 위 영역은 기사제목과 기사링크(href)를 담고있으며, 아래 영역은 이미지 주소(src)를 담고 있습니다.

![image](https://blog.kakaocdn.net/dn/cahXKP/btq7PMnuIwH/zaP3QZAOtLn0HrACazPQk1/img.png)

## 텍스트 추출 .text

- selenium의 텍스트 추출은 아주 쉽습니다. 아래와 같이 선택자(css selector)를 이용해 원하는 부분의 html을 변수에 저장해준 후에, 아래와 같이 for 문과 .text 함수를 이용해 주시면 됩니다.

```python
#step6.뉴스 제목 텍스트 추출

news_titles = driver.find_elements(By.CLASS_NAME, "news_tit")

for i in news_titles:
    title = i.text
    print(title)
```

- 결과는 아래와 같이 출력됩니다.

![image](https://blog.kakaocdn.net/dn/ct1dUn/btq7QvyMZXZ/YZ8hLEY1eP10TG7z8uVT60/img.png)


## 링크 추출 .get_attribute('href')

- 링크를 가져오고 싶을 때, 속성을 가져오는 .get_attribute('href')를 사용합니다. href 속성은 방금 전 가져온 news_titles 변수에 저장되어 있으므로, 따로 한 번더 가져와줄 필요 없이 바로 for문을 써줬습니다.

```python
#step7.뉴스 하이퍼링크 추출

for i in news_titles:
    href = i.get_attribute('href')
    print(href)

```

- 결과는 아래와 같이 10개의 url이 출력되는 것을 확인하실 수 있을거예요.

![image](https://blog.kakaocdn.net/dn/wU9ry/btq7RKWvBaM/DcakCdDB2BI7rm4JeoJk6K/img.png)

## 이미지 추출 .get_attribute('src')

- 다음으로는 이미지 추출입니다. 텍스트나 url 링크를 가져올 때와는 다르게 조금 길지만 어려워 하실 필요없어요.
- 앞서 배우신 것과 같이 이미지 주소(src)를 갖고 있는 html을 news_thumnail 변수에 저장해줍니다.
- 그 다음엔 이미지 다운로드를 위해서 해당 주소들을 리스트(link_thumnail)에 append 함수를 이용해 하나씩 담아주세요.
- 사진을 다운로드 받아서 내 PC에 저장하기 위해서는 저장할 폴더를 만들고, src 주소를 이용해 다운로드 해주면 됩니다.
- 폴더 생성에는 os 모듈과 urllib.request 패키지의 urlretrieve 함수가 필요한데, 모두 다 파이썬 내장 라이브러리이므로 따로 설치해주실 필요 없이 import 해주시면 돼요.

```python 
#step8.뉴스 썸네일 이미지 추출

# 스크롤 내리기 (모든 썸네일 이미지 로딩을 위함)
driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")

time.sleep(2)

#뉴스 썸네일 이미지 다운로드
news_content_div = driver.find_elements(By.CLASS_NAME, 'news_contents')

news_thumbnail = []

for i in news_content_div:

    try:

        thumbnail = i.find_element(By.CLASS_NAME, "thumb")
        news_thumbnail.append(thumbnail)

    except:
        pass

link_thumbnail = [img.get_attribute('src') for img in news_thumbnail]

# 이미지 저장할 폴더 생성
import os

# path_folder의 경로는 각자 저장할 폴더의 경로를 적어줄 것
path_folder = r'D:/images/'

if  not os.path.isdir(path_folder):
    os.mkdir(path_folder)

# 이미지 다운로드
from urllib.request import urlretrieve

i = 0

for link in link_thumbnail:
    i += 1
    urlretrieve(link, path_folder + f'{i}.jpg')
    time.sleep(0.3)

```