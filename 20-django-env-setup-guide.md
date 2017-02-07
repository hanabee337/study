# Django Env Setup
1. 새 가상환경 생성
2. 프로젝트 폴더 생성
3. 프로젝트 폴더 내부에 가상환경 적용
4. 장고 설치
5. ipython 설치
6. django_extension 설치
7. requirement.txt. 저장
8. django-admin startproject mysite로 프로젝트 생성
9. 장고 프로젝트 컨테이너 폴더 이름 django_app으로 변경
10. git 저장소 초기화
11. gitignore 작성(python, pycharm, django 등등)
12. git add -A후, git status로 잘 작동하는지 확인
13. 문제 없으면, 첫 commit push
14. pycharm interpreter 설정
15. shell_plus 실행
16. 추천 
	- .gitignore 파일에 .idea/ 도 추가


< 참고 >
- python manage.py 입력하면 입력가능한 명령 리스트 show
- CSRF : token 값으로 인증확인

- 문자열을 확인해서 어떤 url로 보내는 것이 아니라,
어떤 패턴을 확인해서 반대로 해당 view로 매칭시키는 것이 reversedirect