# Making Django App, Part 6
**Reference** : <http://django-document-korean.readthedocs.io/ko/latest/intro/tutorial06.html>

- 우리는 테스트 된 웹 설문조사 애플리케이션을 구축했으며, 
이제 스타일 시트와 이미지를 추가 할 것입니다.

- 서버에서 생성 된 HTML을 제외하고, 웹 어플리케이션은 
일반적으로 전체 웹 페이지를 렌더링하는 데 필요한 추가 파일 
(예:이미지, JavaScript 또는 CSS)을 제공해야합니다. 
Django에서는 이러한 파일을 “정적 파일” 이라고 부릅니다.

- 소규모 프로젝트의 경우, 웹 서버가 정적 파일을 보관할 수 있기 때문에 
큰 문제는 아닙니다. 그러나 더 큰 프로젝트 – 특히 여러 응용 프로그램으로 구성된 프로젝트 – 의 경우,
각 응용 프로그램에서 제공하는 여러 정적 파일 세트를 다루는 것이
까다로워지기 시작합니다.

- 이것이 django.contrib.staticfiles의 목적입니다.
이것은 각 응용 프로그램(및 여러분이 지정한 다른 위치)의 정적 파일들을 
프로덕션 환경에서 쉽게 제공 할 수있는 단일 위치로 수집합니다.

## 앱의 모양과 느낌을 원하는 대로 바꿔보세요
- 먼저, **```polls 디렉토리```**에 **```static 디렉토리```**를 만듭니다. 
``polls/templates/``안의 템플릿을 찾는 것과 비슷하게 정적 파일을 찾습니다.
-  Django의 STATICFILES_FINDERS 설정은 다양한 소스에서 
정적 파일을 찾는 방법을 알고 있는 파인더 목록을 가지고 있습니다.
기본값 중 하나는 AppDirectoriesFinder 인데,
 INSTALLED_APPS 에서 “정적” 하위 디렉토리를 찾습니다, 
 방금 생성 한 polls 의 경우입니다. 
관리 사이트는 정적 파일에 대해 동일한 디렉토리 구조를 사용합니다.

- 방금 생성 한 ```static 디렉토리``` 안에 ```polls 라는 또 다른 디렉토리```를 만들고,
그 안에 ```style.css``` 라는 파일을 만듭니다. 
즉, ```스타일 시트```는 **```polls/static/polls/style.css```**에 있어야 합니다. 
AppDirectoriesFinder 정적 파일 파인더가 작동하는 방식에 따라 
Django의 정적 파일을 polls/style.css 라고 간단하게 참조 할 수 있습니다. 
이것은 템플릿 경로를 참조하는 것과 유사합니다.

- 그 스타일 시트 (polls/static/polls/style.css)에 다음 코드를 넣으십시오:
```css
>>> polls/static/polls/style.css

li a {
    color: green;
}
```
- 다음으로, polls/templates/polls/index.html의 맨 위에 다음을 추가하십시오

```css
>>> polls/templates/polls/index.html

{% load static %}

<link rel="stylesheet" type="text/css" href="{% static 'polls/style.css' %}" />
```

- {% static %} 템플릿 태그는 정적 파일의 절대 URL을 생성합니다.

- 개발할 때 이것만 하면 됩니다. 
**```http://localhost:8000/polls/```**나 
**```http://127.0.0.1:8000/polls/```**를 새로 고침하면,
질문 링크가 녹색 (Django 스타일!) 인 것을 볼 수 있습니다. 
이는 스타일 시트가 제대로 로드되었음을 의미합니다.

## 백그라운드 이미지를 추가합니다
- 다음으로, 이미지 용 하위 디렉토리를 만듭니다. 
- polls/static/polls/ 디렉토리에 images 서브 디렉토리를 만듭니다. 
- 이 디렉토리 안에 background.gif라는 이미지를 넣으십시오. 
- 즉, 이미지를 **```polls/static/polls/images/background.gif```**에 넣으십시오.

- 그런 다음, 스타일 시트에 추가하십시오 
**```(polls/static/polls/style.css)```**

```css
body {
    background: white url("images/background.gif") no-repeat right bottom;
}
```
- ```http://localhost:8000/polls/```을 새로 고침하면,
화면의 오른쪽 하단에 배경이 표시됩니다.


http://127.0.0.1:8000/admin/polls/
http://localhost:8000/polls/
http://127.0.0.1:8000/polls/
