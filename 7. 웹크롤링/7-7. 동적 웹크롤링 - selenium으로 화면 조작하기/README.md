# 동적 웹크롤링 - selenium으로 화면 조작하기

## Selenium으로 화면 조작하기

- selenium은 원하는 화면 상태에 도달할 수 있도록 웹 브라우저를 조작 가능합니다.
- 예를 들어서, 네이버 메일을 확인하기 위해서 로그인 과정을 거쳐야 한다거나, 유튜브 댓글을 모두 크롤링하는데 스크롤을 내려야지 댓글이 추가적으로 업데이트 되는 상황이 있겠죠.
- 이런 상황에서 원하는 버튼을 클릭 하거나 문자를 입력하는 등의 컴퓨터가 해주어야 하는데 이를 Selenium 패키지가 대신 해줄 수 있습니다.
- 쉽게 말해서 웹 브라우저용 매크로랄까요?
- Selenium으로 화면을 조작하는 전체적인 개념은 다음과 같습니다.

## 개념

- 조작을 원하는 버튼이나 입력창의 html을 파악
- 아래의 두 함수에 html 정보를 입력해서 객체(버튼/입력창 등) 선택
    - find_element(By.ID)
    - find_element(By.CLASS_NAME)
    - find_element(By.XPATH)
    - find_element(By.CSS_SELECTOR)
- 기능 동작 관련 함수로 원하는 기능 조작
    - 클릭 : .click( )
    - 키 입력: .send_keys( )
- 원하는 키워드를 검색하는 아주 간단한 예제를 통해서 어떤 방식으로 사용하는지 보여드리겠습니다.

## 1단계. 원하는 버튼의 html 타겟팅

- 가장 먼저 해줄 일은 크롬을 실행해서 F12를 누르는 것 부터 시작합니다.
- F12를 누르면 지난 강의에서 배우셨 듯이 웹 브라우저 우측에 '개발자 도구'가 나타날 거예요. 그러면 개발자 도구 상단의 화살표 버튼을 눌러서 조작을 원하는 부분을 클릭해주세요.

![image](https://wikidocs.net/images/page/137914/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-10-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_4.45.21.png)

- 검색창에 원하는 키워드를 입력하고 앤터를 눌러주는 것이 이번 예제의 목적이므로 검색창을 타겟팅 할 수 있도록 속성 HTML/CSS 강의 시간에 공부 하셨던 'CSS Selector' 개념을 이용해보겠습니다.
- 방금 전까지 잘 따라오셨다면 아마 개발자 도구에 '검색창'의 html 부분이 나타나 있을텐데요. 우선 빨간색으로 표시된 class 속성값 부분을 더블클릭해서 복사(Ctrl+c)를 해주세요.

> 여기서 잠깐
>
> class명이 gLFyf gsfi와 같이 빈칸이 존재하는 경우는 빈칸을 점(.)으로 변경해주지 않으면 원하는 정보를 제대로 찾지 못합니다. 즉, 클래스명을 gLFyf.gsfi라고 입력해주어야 합니다.

## 2단계. Selenium으로 타겟팅한 html 찾기

- 그 다음으로 해줄 일은 Selenium의 find_element( ) 함수 에 방금 복사해놓은 클래스명 (gLFyf.gsfi)를 ( ) 안에 넣어서 크롬 드라이버가 알아먹을 수 있게 변환해주는 것입니다.
- 이때 클래스명 앞에 붙여주어야 하는 코드가 있는데 바로 로케이터(Locator)라는 것입니다.

![image](https://blog.kakaocdn.net/dn/bY8T05/btsCWMJprLC/ugpcltXKZ3sThUHloQZluk/img.png)

- 제가 주로 초보자분들께 추천드리는 로케이터는 ID, CLASS_NAME, XPATH 총 3가지 입니다. 이것만 잘 쓰셔도 웬만한 사이트는 모두 자동화 가능하거든요.
- 그 전에 먼저 관련 모듈을 import 해주고, 구글 드라이버를 이용해 'Google'까지 접속해줍시다. 아래 코드에 주석을 달아두었으니 그리 어렵진 않으실거예요.

```python
# selenium의 webdriver를 사용하기 위한 import
from selenium import webdriver

# selenium으로 무엇인가 입력하기 위한 import
from selenium.webdriver.common.keys import Keys

# 페이지 로딩을 기다리는데에 사용할 time 모듈 import
import time

# 크롬드라이버 실행
driver = webdriver.Chrome() 

#크롬 드라이버에 url 주소 넣고 실행
driver.get('https://www.google.co.kr/')

# 페이지가 완전히 로딩되도록 3초동안 기다림
time.sleep(3)
```

- 자, 이제 find_element( ) 함수로 chromedriver가 검색창을 찾을 수 있게 해봅시다.

```python
# 검색어 창을 찾아 search 변수에 저장 (By.CLASS_NAME 방식)
search_box = driver.find_element(By.CLASS_NAME, 'gLFyf.gsfi')

# 검색어 창을 찾아 search 변수에 저장 (By.XPATH 방식)
search_box = driver.find_element_by_xpath('//*[@id="google_search"]')
```

## 3단계. 원하는 조작 수행

- 여기까지 하셨으면 Chromedriver가 Selenium 패키지의 find_element 함수를 이용해서 원하는 html을 찾은 상태입니다.
- 이제 남은 일은 원하는 조작을 수행하도록 명령 내리는 일입니다.
- 명령은 간단합니다. 클릭하거나 원하는 키를 입력해주는 것 2가지 입니다.
    - 클릭 : .click( )
    - 키 입력: .send_keys( )

![image](https://blog.kakaocdn.net/dn/cClYng/btriB5X449e/eYEVIap9TG3oc1tlQM4zt1/img.png)


- 그럼 간단히 어떻게 코드로 적용할 수 있는지 알아보겠습니다.

```python
search_box.send_keys('파이썬')
search_box.send_keys(Keys.RETURN)
time.sleep(1)
```

- 사용법 역시 정말 간단합니다.
- 아까 찾았던 검색창(search_box) 변수 다음에 .send_keys('검색어')를 넣어주면 아래와 같은 상태가 되겠죠?

![image](https://blog.kakaocdn.net/dn/5stn5/btrisMxyIiV/TE7T8UklKM7RG4AYSZ3ahk/img.png)

- 그 다음에 search_box.send_keys(Keys.RETURN)을 입력해주면 우리가 검색어를 치고 '엔터키'를 입력해주는 것과 동일합니다.
- 참고로 그림에서 Google 검색 버튼을 우리가 했던 방식으로 타겟팅 해주고 .click( ) 함수로 '마우스 클릭' 해주어도 엔터키를 입력한 것과 동일한 결과를 얻을 수 있습니다.

```python
# click 함수는 ()안에 아무것도 넣지 않으면 좌클릭을 수행
search_button.click()
```
