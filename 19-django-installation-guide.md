# Django Installation guide
1. ```projects``` 폴더에서 ```django``` 폴더를 만든다.
2. ```django``` 폴더로 이동 후, ```tutorial``` 폴더를 만든다.
3. 가상환경 만들기
	```
	$ projects/django/tutorial 폴더로 이동 후,
	```
	```
	$ pyenv virtualenv 3.4.3 django_tutorial
	```
	```
	$ pyenv local django_tutorial
	```
	
4. 장고 설치하기
	```
	pip install django
	```
	
5. 정상적으로 설치가 되었는지 버전 확인
	```
	$ python -m django --version 입력해서
	```
	```
	1.10.5이 나오는지 확인
	```
	- 만약 설치가 제대로 되지 않았다면,
	“No module named django” 과 같은 에러가 발생합니다.
