# 프로젝트 세팅
------
- pipfreeze 하면 가상환경에 설치된 패키지 정보 나온다

- pip freeze > requirements.txt

`>`는 덮어쓰기
`>>`는 붙여넣기

- 레파지토리 관리할때 저 requirements.도 올려줘야 받은 사람이 필요한 가상환경 패키지를 알 수 있다.

-----

### 프로젝트 기본세팅 

- 새로운 가상환경 만들기

```
➜  projects git:(master) ✗ mkdir pip_test
➜  projects git:(master) ✗ pyenv versions
  system
* 3.4.3 (set by /usr/local/var/pyenv/version)
```
- 새로 디렉토리 만들구 버전 확인

```
➜  pip_test git:(master) ✗ pwd
/Users/kizmo04/Dropbox/projects/pip_test
➜  pip_test git:(master) ✗ pyenv virtualenv 3.4.3 pip_test_env
Ignoring indexes: https://pypi.python.org/simple
Requirement already satisfied (use --upgrade to upgrade): setuptools in /usr/local/var/pyenv/versions/3.4.3/envs/pip_test_env/lib/python3.4/site-packages
Requirement already satisfied (use --upgrade to upgrade): pip in /usr/local/var/pyenv/versions/3.4.3/envs/pip_test_env/lib/python3.4/site-packages
➜  pip_test git:(master) ✗ pyenv local pip_test_env
(pip_test_env) ➜  pip_test git:(master) ✗ git init
Initialized empty Git repository in /Users/kizmo04/Dropbox/projects/pip_test/.git/
(pip_test_env) ➜  pip_test git:(master) ✗ vi .gitignore
(pip_test_env) ➜  pip_test git:(master) ✗ cat .gitignore
```

- 새로만들구 로컬에서 가상환경 이거 사용한다고 정해줌 
- git init 하고

- .gitignore도 만들어줌 (.gitignore를 먼저 만들어주지 못하면 나중에 커밋된 것들은 추가되지 않으므로 저장소 다시 지우고 만들어야 할 수 도 있다. 이럴땐 .git폴더 지우고 다시 커밋하면 됨.. 처음부터..)
```python
(pip_test_env) ➜  pip_test git:(master) ✗ pyenv versions
  system
  3.4.3
  3.4.3/envs/pip_test_env
* pip_test_env (set by /Users/kizmo04/Dropbox/projects/pip_test/.python-version)
(pip_test_env) ➜  pip_test git:(master) ✗ pip list
You are using pip version 6.0.8, however version 9.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
pip (6.0.8)
setuptools (12.0.5)
```

- requests랑 beatifulsoup 설치
- 이후 파이참 실행

```
/usr/local/var/pyenv/versions/3.4.3/envs/pip_test_env/bin/python
```
로 파이참에 프로젝트 인터프리터 설정해준다. 

- 리눅스
`/home/<자기유저명>/.pyenv/versions/3.4.3/env/<가상환경이름>/bin/python`

- 맥
`/usr/local/var/pyenvversions/3.4.3/env/<가상환경이름>/bin/python`


- 테스트 코드 파일 만든 후에 코드 파일만 남기고 깃에 커밋하기(커밋 메세지 분리를 위해 차례로커밋함)

- requirements.txt
만들어서 커밋 & 푸쉬

- git reset HEAD~1 
	- 이걸로 커밋내역을 리셋하고 다시 커밋할 수 있다. 단, 남들과 공유한 저장소에서 푸쉬후에 커밋을 이렇게 바꾸면 안됨. 레파지토리 새로 만드는거랑 마찬가지임. 혼자 사용할때만 쓸 수 잇는 방법.


---

### 남이 올린 프로젝트때 클론할때

```
➜  projects git:(master) ✗ mkdir sample
➜  projects git:(master) ✗ cd sample
➜  sample git:(master) ✗ pyenv versions
  system
* 3.4.3 (set by /usr/local/var/pyenv/version)
  3.4.3/envs/pip_test_env
  fc-python
  pip_test_env

```
- 테스트를 위해 새로 디렉토리 생성

```
➜  sample git:(master) ✗ git clone https://github.com/kizmo04/pip_test.git
Cloning into 'pip_test'...
remote: Counting objects: 14, done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 14 (delta 2), reused 14 (delta 2), pack-reused 0
Unpacking objects: 100% (14/14), done.
```

- 아까 만들어둔 저장소를 클론.
- 다른데서 만든 프로젝트를 받앗다고 가정하구,,,

```
➜  sample git:(master) ✗ cd pip_test
➜  pip_test git:(master) pyenv virtualenv 3.4.3 cloned_project
Ignoring indexes: https://pypi.python.org/simple
Requirement already satisfied (use --upgrade to upgrade): setuptools in /usr/local/var/pyenv/versions/3.4.3/envs/cloned_project/lib/python3.4/site-packages
Requirement already satisfied (use --upgrade to upgrade): pip in /usr/local/var/pyenv/versions/3.4.3/envs/cloned_project/lib/python3.4/site-packages
➜  pip_test git:(master) pyenv local cloned_project
(cloned_project) ➜  pip_test git:(master) pip list
You are using pip version 6.0.8, however version 9.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
pip (6.0.8)
setuptools (12.0.5)
```
- 클론받은 폴더에 가서 가상환경 다시 만듦. 근데 프로젝트에 사용된 패키지는 설치가 안돼있다

```
(cloned_project) ➜  pip_test git:(master) python pip-test.py
Traceback (most recent call last):
  File "pip-test.py", line 5, in <module>
    import requests
ImportError: No module named 'requests'
```

- 그래서 실행안됨!!

```
(cloned_project) ➜  pip_test git:(master) pip install -r requirements.txt
You are using pip version 6.0.8, however version 9.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
Collecting beautifulsoup4==4.5.3 (from -r requirements.txt (line 1))
  Using cached beautifulsoup4-4.5.3-py3-none-any.whl
Collecting requests==2.13.0 (from -r requirements.txt (line 2))
  Using cached requests-2.13.0-py2.py3-none-any.whl
Installing collected packages: requests, beautifulsoup4


Successfully installed beautifulsoup4-4.5.3 requests-2.13.0
```

- 하지만 요로면 실행됨!!

- 그래서 requirements를 꼭 만들어줘야 한다. 이후 프로젝트는 실행 잘됨

- 하지만 파이썬 버전은 어떻게 프로젝트에 알려주냐면

- README.md에 명시한다.

