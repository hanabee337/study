# Facebook 로그인 추가
### [앱이나 웹사이트에 Facebook 로그인 추가하기](https://developers.facebook.com/docs/facebook-login) 

### [로그인 플로 직접 빌드](https://developers.facebook.com/docs/facebook-login/manually-build-a-login-flow) 
---
- SDK를 사용하지 않고 앱의 브라우저 기반 로그인을 구현해야 하는 경우 브라우저 리디렉션을 사용하여 로그인 플로를 직접 빌드할 수 있습니다. 이 가이드에서는 로그인 플로의 각 단계를 설명하고 SDK를 사용하지 않고 각 단계를 구현하는 방법을 보여줍니다.
	- [로그인 상태 확인](https://developers.facebook.com/docs/facebook-login/manually-build-a-login-flow#checklogin)  
	- [사용자 로그인 유도](https://developers.facebook.com/docs/facebook-login/manually-build-a-login-flow#login)  
	- [ID 확인](https://developers.facebook.com/docs/facebook-login/manually-build-a-login-flow#confirm)  
	- [액세스 토큰 및 로그인 상태 저장](https://developers.facebook.com/docs/facebook-login/manually-build-a-login-flow#token)  
	- [사용자 로그아웃 유도](https://developers.facebook.com/docs/facebook-login/manually-build-a-login-flow#)  

#### 사용자 로그인 유도
- **로그인 대화 상자 호출 및 리디렉션 URL 설정**
앱에서 로그인 대화 상자를 표시할 엔드포인트로 리디렉션을 시작해야 합니다.  

![](imgs/facebook-login-redirect.png)  

1. 그러기 위해선 먼저, **app-id**를 만들어야 함.  
	- 위의 ```로그인 플로 직접 빌드```의 ```사용자 로그인 유도```로 접속 후, 우측 상단에 ```내 앱```이동. 그리고 ```새 앱 추가```선택
	-  새 앱 ID만들기에서 입력 후, ```앱 ID 만들기``` 버튼 클릭   
![](imgs/facebook-app-id.png)   

	- 추가 보안문자 입력 후, 하기 그림과 같이 앱 ID가 만들어 진 것 확인  
![](imgs/facebook-app-id-create.png)  

	- 이 ```앱 ID```가 youtube의 **API_KEY** 처럼 코드 상에선 ```.conf 폴더```에 ```settings_local.json 파일```에 별도 처리되는 정보이다.
	- 코드상에선 다음과 같다.  
	![](imgs/facebook-app-id-code.png)   
	
	- 기본 설정하기
		- member app을 만들고, AbstractUser를 상속 받는  MyUser 구현
		- settings.py에 INSTALLED_APPS에 등록하고, AUTH_USER_MODEL = 'member.MyUser' 입력
		- 이후 Migration
		- settings.py 기본 설정하기(templates,static,media path 설정)
	- 여기서 앱 ID와 마찬가지로 별도 관리를 해야되는 값이 있는데, 바로 **SECRET_KEY**값이다.
		- 이 값은 production에 절대로 포함되면 안되는 값.
		- Django는 이 값을 이용해서, 해싱등을 사용하여 패스워드의 고유 값을 만드는데 사용하기 때문이다.

	![](imgs/facebook-django-secret-key.png)  

	![](imgs/facebook-django-secret-key-settings.png)  
	
	- 마지막으로 하나 더 별도 관리해야 하는 값이 있는데, ```secret_code``` 값이다. 방법은 하기 그림과 같이 ```보기``` 버튼을 누른 후, 패스워드 입력하면 표시가 된다. 이 값을 ```app_id와 함께 관리```한다.  
	
	![](imgs/facebook-app-secret-code.png)  

	- 앱 ID를 view를 통해 template에 전달
	![](imgs/facebook-app-id-html.png)  

2. **redirect-uri**
	- a tag를 이용하여 이 경로로 이동하면, 페이스북 로그인 할 수 있는 창이 뜬다. 
	그 창에서 로그인을 했을 때, 원래 로그인하려고 했었던 사이트에다 정보를 제공해줘야 하는데, 그 때 ```정보를 받을 url```을 ```redirect uri```에 적어준다. 우리가 하기와 같이 임의로 url을 'localhost의 member/login/facebook/' 으로 정하였다.(코드 참조)
	![](imgs/facebook-redirect-uri.png)   
