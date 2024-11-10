# 동적 웹크롤링 - selenium 소개 및 기초사용법

## Selenium 패키지란?

- selenium 패키지는 chromedriver를 제어하거나 원하는 정보를 얻기 위해 사용합니다.
- 크롤링을 하다보면 무엇인가 입력하거나 특정 버튼을 눌러야 하는 상황이 발생합니다. 사람이 그러한 행동을 하는 대신 컴퓨터가 할 수 있도록 해주는 패키지가 selenium입니다.
- selenium 패키지도 웹 정보를 크롤링하는 것이 가능하기 때문에 저는 웹 크롤링은 거의 selenium을 패키지를 사용하는 편입니다.

## 설치 방법
- vscode의 터미널창에서 아래와 같이 입력하면 됩니다. 만약 anaconda를 사용하신다면 pip 혹은 conda 명령어를 둘 다 사용가능하시고, python 공식 
- 홈페이지를 통해 python을 설치하셨다면 아래의 코드를 사용하시면 됩니다.

```python
pip install selenium
```

## 사용 방법

- 디테일한 사용 방법은 다음 시간부터 알아보도록 하고, 이번 시간에는 크롬 드라이버를 이용해서 원하는 사이트에 접속하는 것 까지 해보겠습니다.

### 관련 패키지 import

- selenium 패키지를 사용하기 위해서는 아래의 두 가지 모듈을 import 해주어야 합니다.
- 추가적으로 페이지 로딩을 기다리는데에 사용할 time 모듈도 import 해줍니다. 이 모듈은 파이썬 내장 라이브러리에 포함되어 있어 별도 설치는 필요 없습니다.

```python
# selenium의 webdriver를 사용하기 위한 import
from selenium import webdriver

# selenium으로 키를 조작하기 위한 import
from selenium.webdriver.common.keys import Keys

# 페이지 로딩을 기다리는데에 사용할 time 모듈 import
import time
```

### 크롬 드라이버 실행

- 관련 패키지를 불러왔으면 다음으로 해줄 일은 크롬 드라이버를 이용해서 크롬을 실행해주는 일입니다.
- 크롬 드라이버는 컴퓨터가 크롬 웹 브라우저를 다룰 수 있도록 해주는 프로그램으로 구글에서 제공 해줍니다. 크롬 드라이버는 코드를 실행 시키시면 자동으로 
- 다운로드 되니 별도 설치가 필요 없습니다. (4.6 버전부터 크롬드라이버 별도 다운로드 및 경로 설정 불필요)

```python
# 크롬드라이버 실행
driver = webdriver.Chrome() 

#크롬 드라이버에 url 주소 넣고 실행
driver.get('https://www.google.co.kr/')

# 페이지가 완전히 로딩되도록 3초동안 기다림
time.sleep(3)
```

- 크롬 드라이버로 구글 웹페이지에 접속한 상태

![image](https://wikidocs.net/images/page/137914/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-10-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_4.13.06.png)


