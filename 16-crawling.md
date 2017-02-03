#pycharm에서 환경 설정
1. pycharm 실행하여 home/hanabee2/projects/python/crawling에서 craw.py 파일 생성

2. alt + F12 : Terminal 창 띄우기
3. pyenv version 입력하여 가상환경(virtualenv)이 적용된 터미널 확인(pycharm 하단의 terminal에서 확인)
4. pycharm 하단의 terminal에서 하기 입력

5. install beautifulsoup4
	- $ pip install beautifulsoup4
6. install requests
	- $ pip install requests
7. 해석기 설치하기
- 뷰티플수프는 파이썬 표준 라이브러리에 포함된 HTML 해석기를 지원하지만, 또 수 많은 제-삼자 파이썬 해석기도 지원한다.
그 중 하나는 lxml 해석기이다. 설정에 따라, 다음 명령어들 중 하나로 lxml을 설치하는 편이 좋을 경우가 있다. 
	- $pip install lxml
8. pycharm 환경에서 crawl.py 파일을 open한 후, import requests 입력.
정상동작 확인은 다음 라인에서 requests 모듈의 함수를 입력해서
import가 주황색으로 바뀌면 정상적으로 import된 것임.

```pycharm
import requests
requests.get('abc')
```
- Pycharm에서
```
setting -> Project: Crawling -> Project Interpreter에서는, virtualenv로 설정하고
settings -> Build -> Console -> Python Console 에서는 virtualenv가 아닌 .pyenv/version/~  으로 설정
```
- 참조: <https://www.crummy.com/software/BeautifulSoup/bs4/doc/>
- 참조: <http://docs.python-requests.org/en/master/user/quickstart/#passing-parameters-in-urls>

### local에 가상 환경 지정
- pyenv local fc-python
- 시스템에 있는 python을 건드리지 않기 위해 pyenv 설치 및 설정
- python & pyenv & virtualenv에 대해 의미 파악 확인.

### html parser(해석기)
- <https://www.crummy.com/software/BeautifulSoup/bs4/doc/>
- Beautiful Soup supports the HTML parser included in Python’s standard library, but it also supports a number of third-party Python parsers. One is the lxml parser.
- pip install lxml

### 실습
- projects/python/crawling/crawl.py