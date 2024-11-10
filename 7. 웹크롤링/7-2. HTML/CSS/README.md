# HTML/CSS

- 우리가 어떤 웹사이트를 만나던 어떤 종류의 자료든 크롤링 할 수 있으려면, HTML과 CSS에 대한 개념을 이해할 필요가 있습니다.
- 두 언어만 공부하는데에도 각각 책이 한 권 씩일 정도로 내용이 많으므로, 최소한의 필요한 부분만 공부해 보도록 하겠습니다.



## HTML 구조
- html은 기본적으로 아래와 같은 구조를 가집니다.
- 한마디로 html은 태그로 감싸진 속성과 내용들의 모음입니다.

![이미지](https://blog.kakaocdn.net/dn/cgAqnI/btq08uOFu49/KmhFDOWzwIZwlSh6zCFmj1/img.png)


### 태그 이름
- 태그는 그 종류가 다양하며, 각 태그마다 의미하는 바가 다릅니다. 우리가 웹크롤링을 하면서 자주 볼 수 있는 태그는 아래와 같습니다.
- 한 번에 다 이해하려고 하실 필요는 없습니다! 필요할 때마다 해당 표를 참고하시면 되니깐 여러가지의 태그가 있다라는 정도만 이해하고 넘어가시면 되겠습니다.
![이미지](https://wikidocs.net/images/page/137929/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-08-16_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_4.39.14.png)

### 속성명
- html은 수 많은 태그로 이루어져 있어서 동일한 태그가 무수히 많이 사용됩니다.
- 그래서 각 태그들을 구분해주기 위해서 속성을 부여 해줍니다.
- 각 태그별로 속성이 다양하지만 꼭 기억해야할 속성 2가지는 id와 class입니다.

##### ID

- 하나의 웹페이지에 하나만 쓸 수 있는 고유한 이름으로 <태그이름 id="속성값">와 같이 쓰임

#### CLASS

- 비슷한 형태를 가진 요소에 여러번 사용할 수 있는 이름으로 <태그이름 class="속성값">와 같이 쓰임

### 속성값과 내용
- 프로그래머가 정해주기 나름

## CSS 구조
- css는 html로 만들어진 밋밋한 화면을 예쁘게 꾸며주는 역할을 합니다.
- css는 html 특정 태그를 지목해서 속성값(글자색, 크기, 폰트, 배경색 등등)을 넣어 주는 것이라 생각하시면 돼요.
- 이때 css가 특정 태그를 지목하는 방식, 이 규칙을 알게되면 우리가 원하는 데이터를 감싸고 있는 태그를 지목해서 그 안의 데이터를 가져올 수 있는 것입니다.

![이미지](https://blog.kakaocdn.net/dn/bnza6W/btq08vtlK9C/oTW3vjynBppfC8pKxfHJu0/img.png)

### CSS Selector
- CSS 코드는 위와 같이 선택자(selector)와 선언부(declaratives)로 구성됩니다.
- 여기서, 선택자라는 것이 우리가 주목해야할 개념입니다.
- 간단히 정리하면 아래와 같습니다.

![이미지](https://wikidocs.net/images/page/137929/%EC%BA%A1%EC%B2%98.PNG)

#### 쉬운 이해를 위해서 CSS 선택자를 어떻게 활용하는지 예시를 보여드리겠습니다.

-  크롬 브라우저로 네이버에 접속
- 개발자 도구(단축키:F12)를 열어서, 검색창의 HTML을 확인
- HTML을 우클릭해서, Copy - Copy selector를 클릭
- 코딩창의 원하는 위치에 붙여넣기(Ctrl+V)

![image](https://blog.kakaocdn.net/dn/3sEtx/btrcNMo0rG7/ZfQZq5NkFDYO5YfBx721rk/img.gif)


- 이렇게 하면 #query라는 css selector가 불러와지고, 이 선택자를 아래 코드들의 괄호 안에 넣으시면 원하시는 동작을 수행하거나 데이터를 가져올 수 있습니다.

```python
# selenium으로 id가 query인 html 1개 선택(여러개 일 때 가장 위의 요소 선택)
driver.find_element_by_css_selector('#query')

# selenium으로 id가 query인 html 모두 선택
driver.find_elements_by_css_selector('#query')
```

- 개인적으로 CSS selector 개념이 직관적이고 이해하기 쉬워서 주로 이용할 예정입니다.
- 하지만 인터넷에 돌아다니는 웹 크롤링 관련 코드들은 CSS selector를 사용하지 않고 html 태그를 선택하는 경우도 있답니다.