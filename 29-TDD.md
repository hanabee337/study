# TDD 테스트 주도 개발 실습
- 테스트 주도 개발(Test-driven development TDD)은 매우 짧은 개발 사이클을 반복하는 소프트웨어 개발 프로세스 중 하나이다
- 소프트웨어 개발 프로세스의 하나. 
일단 개발할 것을 정의한 후, 해당 사항에 대한 테스트를 먼저 작성. 
- 그리고 그 테스트를 통과할 수 있는 실행코드를 작성하는 순서로 개발을 진행하는 기법.

### 기능 테스트 vs 단위 테스트
1. 기능 테스트 (functional test)
	- 외부 사용자의 관점에서 애플리케이션의 외부 동작을 테스트
	- 실제 web-browser를 실행해서 애플리케이션이 어떻게 동작하는지 사용자 관점에서 확인
	
2. 단위 테스트 (unit test)
	- 개발자의 관점에서 애플리케이션의 내부 동작을 테스트
	- 구현 코드의 개별 단위의 적합성, 정확성을 확인하기 위한 방법
	
### 테스트 개발 순서
1. 기능 테스트를 작성하여, 새로 개발할 기능을 정의한다.
2. 하나의 기능에 대해 있어야 할 단위 테스트를 작성한다.
3. 단위 테스트를 하나씩 만족할 수 있도록 코드를 작성한다. 
모든 코드는 적어도 하나의 단위테스트에 의해 테스트 되어야 한다.
4. 모든 단위 테스트를 통과 후, 기능테스트를 통과하는지 확인한다.

### 관련 패키지
 - WebDriver
	- 단순한 API들로 구성된 개발자 중심의 Web UI 테스트 자동화 도구
```
# Chrome 다운로드 및 설치
- chrome이 이미 설치되어있다면, skip
> wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
> sudo dpkg -i --force-depends google-chrome-stable_current_amd64.deb

# ChromeDriver 다운로드 및 설치
> LATEST=$(wget -q -O - http://chromedriver.storage.googleapis.com/LATEST_RELEASE)
> wget http://chromedriver.storage.googleapis.com/$LATEST/chromedriver_linux64.zip

# ChromeDriver의 심볼릭 링크 생성
> unzip chromedriver_linux64.zip && sudo ln -s $PWD/chromedriver /usr/local/bin/chromedriver
```	
- Selenium
	- WebDriver를 사용하는 브라우저 자동화 툴. 
	- 테스트나 브라우저 기반의 작업을 코드로 실행할 수 있도록 해준다.
```
> pip install selenium
```
[WebDriver 와 Selenuim 참조 문헌](http://wiki.gurubee.net/pages/viewpage.action?pageId=6259762#Selenium%EC%9D%84%EC%9D%B4%EC%9A%A9%ED%95%9CUI%ED%85%8C%EC%8A%A4%ED%8A%B8-4.1WebDriver%EA%B0%9C%EC%9A%94) 


### TDD( 클린 코드를 위한 테스트 주도 개발)
- 24p
	- **```Dajngo```**는 ```코드를 앱 형태로 구조화```하도록 도와준다.
	- **```앱```**은 코드를 구조화하기 좋은 수단	
- 25p
	- **```기능 테스트 vs 단위 테스트```**
		- 기능 테스트 : ```상위 레벨```의 개발 주도
		- 단위 테스트 : ```하위 레벨``` 주도
- 27p
	- django의 ```주요 역할```은 일반적인 웹 서버처럼 사용자가 특정 url을 요청했을 때, 어떤 처리를 할지 결정하는 것.
	- ```django의 처리 흐름```
		1. 특정 url에 대한 http 요청을 받는다.
		2. django는 특정 규칙을 이용해서 해당 요청에 대한 어떤 뷰 함수를 실행할지 결정한다. 
		3. 이 뷰 기능이 요청을 처리해서 HTTP 응답으로 반환한다.
		
- 28p
	- ```resolve```는 django 내장 함수로, ```url을 해석해서 일치하는 뷰 함수```를 찾는다.
	
- 30p
	- ```Traceback 읽기```
	- 문제 있는 코드를 확인할 때, 일반적으로 사용하는 4단계 과정이 있다.
- 31p
	- django는 ```urls.py```라는 파일을 이용해서 어떻게 ```URL을 뷰 함수에 맵핑할지 정의```한다.
	- ```url항목```은 정교 표현으로 시작하며, ```어떤 url을 해석해서 어떤 함수로 요청을 보낼지를 정의```한다.
	
- 34p
	- ```뷰를 위한 단위 테스트```
		- 뷰를 위한 테스트를 작성할 때는 단순히 빈 함수를 작성하는 것이 아니라, HTML 형식의 실제 응답을 반환하는 함수를 작성해야 한다.
		- ```단위 테스트```는 기능 테스트에 의해 파생되며, 더 실제 코드에 가깝다.

- 35p
	- ```단위 테스트 : 코드 주기```
		1. 터미널에서 단위 테스트를 실행해서 어떻게 실패하는지 확인한다.
		2. 편집기상에서 현재 실패 테스트를 수정하기 위한 최소한의 코드를 변경한다.
		
- 38p
	- **```3장 정리```**
		- Django 앱 실행
		- Django 단위 테스트 실행자
		- 기능 테스트와 단위 테스트의 차이
		- Django URL 해석 및 urls.py
		- Django 뷰 함수 및 요청, 응답 객체
		- 기본 HTML 반환
		
		- 기능 테스트 실행
			- python functional_test.py
		- 단위 테스트 실행
			- python manage.py test
		- 단위 테스트: 코드 주기
			1. 터미널에서 단위 테스트 실행
			2. 편집기에서 최소 코드 수정
			3. 1~2 반복
- 45p
	- ```단위 테스트```는 로직이나 흐름 제어, 설정 등을 테스트하기 위함

	- **```refactoring```**이란 ```기능(결과물)은 바꾸지 않고, 코드 자체를 개선하는 작업```을 말한다.

- 47p
	- Traceback 분석 연습

- 49p
	- .decode()는 문자열과 문자열을 서로 비교

- 50p
	- ```refactoring에 관해```
		- ```리팩토링 시```에는 앱 코드와 테스트 코드를 ```한 번에 수정하는 것이 아니라 하나씩 수정해야 한다.```

- 53p
	- TDD 프로세스
		- 기능 테스트
		- 단위 테스트
		- 단위 테스트 + 코드 주기(Unit test-code cycle)
		- 리팩토링
- 54p
	- TDD 프로세스 흐름도
		- 먼저 기능 테스트를 작성하고 실패하는지 확인한다.
		- **```기능 테스트```**는 애플리케이션이 동작하는지 아닌지를 판단하기 위한 궁극의 수단.
		- **```단위 테스트```**는 이 판단을 돕기 위한 툴
# 5장
- 60p
	- POST 요청을 전송하기 위한 Form 연동

-  63p
	- 서버에서 POST 요청 처리

- 64p
	- 파이썬 변수를 전달해서 템플릿에 출력하기

- 73p
	- Django에선 ORM의 역할이 데이커베이스 모델을 만드는 것.
	- Migration
		- models.py 파일에 적용된 내용을 기반으로, 사용자가 테이블과 칼럼을 삭제 및 추가할 수 있게 해줌.
		- 상용 서버에 배포한 DB 업그레이드 시 유용하다.
		
- 74p
	- model.Model로부터 상속한 클래스는 데이터베이스의 테이블 역할을 한다.
	- 클래스(DB)가 생성될 떄, 키 역할을 하는 ID 속성이 기본으로 생성된다.
	- 하지만, 다른 칼럼들은 직접 정의해야 한다.
- 75p
	- 신규 필드는 신규 Migration을 의미한다.

- 79p
	- POST 후에 redirection
		- POST 후에는 항상 redirection하라는 말이 있다.
		- 이번 단위 테스트는 POST 요청을 저장해서 돌아온 응답을 rendering 하는 것이 아니라, 홈페이지로 다시 redirection 하기 위함.

- 84p
	- Migration을 이용한 운영 DB 생성하기
		- Django는 단위 테스트를 위해 특수한 DB를 생성한다.
		따라서, 단위 테스트는 통과해도 기능 테스트에서 문제가 발생할 수 있다.
	- SQLite DB는 디스크상에 있는 파일 형태의 DB로, 기본 프로젝트 디렉토리에 db.sqlite3라는 파일로 자장하도록 settings.py에 설정되어 있다.
	- 데이터 베이스는 models.py를 이용하며, migration 파일을 생성한다.
	
- 87p
	- 5장 정리
		1. Form을 설정하고 POST를 이용해서 신규 작업 아이템을 목록에 추가
		2. 간단한 DB 모델을 구축해서 작업 아이템 저장
		3. 적어도 세 가지 이상(?)의 FT 디버깅 기술 적용
		
# 6장
- 96p
	- REST (Representational State Transfer)
		- 웹 설계 방법 중 하나
		- 일반적으로 웹 기반 API를 이용해서 설계하도록 유도
		- 데이터 구조를 URL 구조에 일치시키는 방식
	
- 99p
	- 메타 주석(##)
		- 테스트가 어떻게 동작하는지 설명하기 위해 사용

- 111p
	- Dajngo 테스트 클라이언트가 뷰 함수에서 약간 다른 방식을 동작하기 때문이다. 즉 도메인을 상대 URL에 추가하는 Django 스택을 사용하기 때문.(?) - 이해 안됨
	
	
- 