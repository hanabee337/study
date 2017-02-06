# Django Installation guide

#### 1. ```projects``` 폴더에서 ```django``` 폴더를 만든다.

#### 2. ```django``` 폴더로 이동 후, ```tutorial``` 폴더를 만든다.

#### 3. 가상환경 만들기
```
	1. $ projects/django/tutorial 폴더로 이동 후,
	2. $ pyenv virtualenv 3.4.3 django_tutorial
	3. $ pyenv local django_tutorial
```
	
#### 4. 장고 설치하기
```
	pip install django
```
	
#### 5. 정상적으로 설치가 되었는지 버전 확인
```
	1. $ python -m django --version 입력해서
	2. 1.10.5이 나오는지 확인
```
	- 만약 설치가 제대로 되지 않았다면,
	“No module named django” 과 같은 에러가 발생합니다.
#### 6. Django Project 생성
```
	django-admin startproject mysite
```

#### 6. 프로젝트 컨테이너 폴더명 변경
```
mv mysite django_app
```

프로젝트명과 프로젝트를 담고 있는 폴더명(프로젝트 컨테이너 폴더)은 별개로 취급된다.  
Django에서 프로젝트 생성 시 기본적으로 프로젝트명과 프로젝트를 담고 있는 폴더명을 일치하게 생성해주는데, 
처음에는 헷갈릴 수 있으므로 프로젝트를 담고 있는 폴더명은 다르게 바꾸어준다.

정리하면 아래와 같은 구조를 사용한다.

```
(Project name) <Repository directory>
└── django_app <Django project directory>
    ├── manage.py
    └── (Project name) <Settings Directory>
        ├── __init__.py
        ├── settings.py
        ├── urls.py
        └── wsgi.py
```

#### 7. Pycharm에서는 Repository Directory레벨로 프로젝트 열기
- 해당 레파지토리는 장고 프로젝트만 관리된다는 전제이므로 
해당 레벨로 프로젝트 열기

#### 8.가상환경을 Pycharm에 설정
```
Preferences -> Project -> Project Interpreter
-> /home/hanabee2/.pyenv/versions/3.4.3/envs/django_tutorial/bin/python
```

#### 9. Git설정
- Repository Directory레벨에서 설정


