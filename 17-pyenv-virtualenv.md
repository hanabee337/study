# pyenv 환경 실습
## 내가 작업하고 있는 환경을 github에 올린 것을 누군가가 받아서 사용하려고 할때를 가정하고 실습한 내용
### 기본적인 내용은 13_pyenv_virtualenv_iPython_install_guide.md를 참조바람
```html
<https://github.com/hanabee337/study/blob/master/13_pyenv_virtualenv_iPython_install_guide.md>
```

$pip freeze : 내가 설피한 환경들을 보여줌

$ pip freeze > requirement.txt
txt 파일에 저장

해당 버전에서 동작한다는 것을 보장해서 git에 올리기 위해
python이 있는 폴더에서 $pip freeze함.
하면 현재 버전들을 list-up해줌.

requirements.txt도 버전 관리를 해야함.

pip-test 폴더 새로 생성

github에서 새 repo 만듬.

.gitignore 파일, .idea/도 생성이 되었음.왜지?
 
add하고 push 함.

sample 폴더에서 git clone을 해옴.
 
python pip-test.py 실행시
requests가 없어서 import 에러가 나야함.
그래서, pip install -r requirements.txt를 설치하면
import 시 발생했던 에러가 해결이 된다.

Q) 파이선 버전은 git clone한 사람이 어케 알까?
A) README 파일에다가 inform해주기.




#virtualevn가 지워졌으므로 python 폴더용 가상환경 설정을 해주어야 함
1. pyenv virtualenv <version> <env_name> 으로 환경생성
예 ) $ pyenv virtualenv 3.4.3 fc-python
2. 해당 폴더에서 pyenv local fc-python으로 가상환경 사용 설정
예) projects/python 에서
$ pyenv local fc-python

3. pyenv versions로 설정 적용되었는지 확인, pip list로 새 가상환경 상태인지 확인
$ pyenv
4. pip install -r requirements.txt.로 패키지 설치

5. 위와 별개로 projects/python/class 폴더에만 사용되는 가상환경 적용해보기.

6. pyenv uninstall <가상 env_name>
예) pyenv uninstall closed_projects
그렇게 하면, 가상과 물리 모두 삭제가 됨
3.4.3/env/closed_project
closed_projects
두 개가 모두 없어짐.
pyenv versions로 확인 가능


pip install ipython도 지워졌으므로, 설치를 다시 해줘야 한다.

