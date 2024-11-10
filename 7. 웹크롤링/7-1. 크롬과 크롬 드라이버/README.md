# 크롬과 크롬 드라이버

오늘은 웹 크롤링을 위한 준비 단계로 크롬과 크롬드라이버를 설치해보겠습니다.

## 크롬을 사용하는 이유

## 크롬 버전 확인 방법

- 크롬을 설치하셨다면 버전을 확인할 필요가 있습니다. 크롬 드라이버를 다운로드 받을 때 크롬의 버전과 일치하는 것을 받아줘야 정상 작동하니까요.
- 크롬 창을 열면 우측상단에 (...) 표시가 보이실겁니다.
- 클릭해주시면 아래와 같이 창이 나오는데 도움말 - Chrome 정보를 클릭해 주세요.
  > 한동안 웹크롤링을 하지 않다가 실행하시면 되던 코드가 실행되지 않을 때가 있습니다.
  >
  > 그 때는 크롬 버전에 비해 크롬 드라이버가 예전 것일 확률이 높으니, 크롬 드라이버를 최신 것으로 다시 다운받아서 교체해주시면 됩니다.

## 크롬드라이버 설치 방법

- 뒤에서 배울 selenium이라는 패키지가 2022년 4월에 4.6 버전으로 업데이트 되기 전까지는 크롬 드라이버를 매번 크롬 버전에 맞춰서 설치해주어야 했지만, 더 이상 그런 번거로운 일을 하지 않아도 됩니다.
- 따라서 예전에 설명드렸던 크롬 드라이버 설치에 대한 내용은 더 이상 필요 없어 졌기 때문에 삭제하였습니다.
- 다만, 4.6 보다 더 오래된 버전을 사용하시는 경우에는 다음과 같은 에러가 출력될 수 있습니다.

```
selenium.common.exceptions.SessionNotCreatedException: Message: session not created: This version of ChromeDriver only supports Chrome version 106

Current browser version is 116.0.5845.111 with binary path C:\Program Files\Google\Chrome\Application\chrome.exe
```

- 이런 경우에는 selenium을 최신 버전으로 업그레이드 한 후, VSCODE를 종료했다가 실행하셔야 합니다. 최신 버전 업그레이드는 터미널 창이나 Jupyter의 셀에서 아래 명령어를 입력하시면 됩니다.

```python
pip install --upgrade selenium
```
