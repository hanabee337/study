# Module
### module
- 모듈이란 함수나 변수 또는 클래스 들을 모아 놓은 파일이다.
- 지금까지 shell에서 진행한 실습의 경우, 하나의 모듈 내부에서 작업한 것으로 취급된다.
- python 파일은 각각 하나의 module로 취급된다.

### import 실습
- import의 사용 방법
```
import 모듈이름
```
- 모듈이름은 ```.py```를 제거한 파일명.
- 모듈 함수를 사용하는 또 다른 방법
```
from 모듈이름 import 모듈함수
```
or
```
from 모듈이름 import *
```

- module/shop.py
```python
def buy_item():
    print('Buy item!')

buy_item()
```
- module/game.py
```python
def play_game():
    print('Play game!')

play_game()
```
- module/lol.py
```python
import game
import shop

print('= Turn on game =')
game.play_game()
shop.buy_item()
```


### _name__변수
- ```lol.py```가 실행될 때, ```game```과 ```shop```이 import되는 순간 해당 코드가 실행되어 버리는 문제가 있다.
- 각 모듈은 자신의 이름을 가지며, 모듈 이름은 모듈의 전역변수 **\_\_name\_\_**에서 확인 할 수 있다.
- 파이썬 인터프리터가 실행한 모듈의 경우, **\_\_main\_\_**이라는 이름을 가진다. 따라서 python <파일명>으로 실행한 경우에만 동작할 부분은 if문으로 감싸준다.

- module/shop.py
```python
def buy_item():
    print('Buy item!')

if __name__ == '__main__':
    buy_item()
```
- module/game.py
```python
def play_game():
    print('Play game!')

if __name__ == '__main__':
    play_game()
```
- 다시 lol.py를 실행해본다.

### 커맨드라인에서 인자 전달
- ```프로그램 실행 시 인자를 전달 할 수 있다```
- 파이썬의 ```내장 sys모듈```의 ```argv```리스트에서 확인 할 수 있다.
- 리스트의 첫 번째 항목은 모듈명이 전달되므로, ```2번째 항목부터 전달``` 된 값을 확인 할 수 있다.

## [모듈을 불러오는 또 다른 방법]
### 1. from 을 사용해 module의 함수를 직접 import
- ```import 모듈명```의 경우, 모듈의 이름이 전역 네임스페이스에 등록되어 ```모듈명.함수```로 사용가능하다.
- 모듈명을 생략하고 모듈 내부의 함수를 쓰고 싶다면, ```from 모듈명 import 함수명```으로 불러들일 수 있다.
### 2. from module명 *을 사용해 module 내 모든 식별자(함수,변수) import
- ```from 모듈명 import``` 또는 ```import 모듈명```에서, 같은 모듈명이 존재하거나 혼동 될 수 있을 경우, 뒤에 ```as```를 붙여 사용할 모듈명을 변경할 수 있다.
### 3. sys.path.append(모듈을 저장한 디렉터리) 사용하기
### 4. PYTHONPATH 환경 변수 사용하기
참조 : <https://wikidocs.net/29>

# Package
- **패키지**는 ```모듈들을 모아 둔 특별한 폴더```를 뜻한다.
- 폴더를 패키지로 만들면 ```계층 구조를 가질 수 있으며, 모듈들을 해당 패키지에 모을 수 있는 역할```을 한다.
- 패키지를 만들 때는 패키지로 사용할 폴더에 **\_\_init\_\_.py**파일을 넣어주면, 해당 폴더는 패키지로 취급된다. (비어있어도 무관하다)
- 패키지는 모듈과 동일하게 import할 수 있다.
### \_\_init\_\_.py의 용도
- ```__init__.py 파일```은 해당 디렉터리가 패키지의 일부임을 알려주는 역할을 한다.
- 패키지에 포함된 디렉터리에 \_\_init\_\_.py 파일이 없다면 패키지로 인식되지 않는다.
- 그러나, python3.3 버전부터는 \_\_init\_\_.py 파일 없이도 패키지로 인식이 된다. 하위 버전 호환을 위해 생성하는 것이 안전하다.
- init.py 파일에서 미리 지정해 놓으면,  해당 패키지에서 자동으로 loading을 해주는 역할도 한다.

### *, __all__
- 패키지에 포함된 하위 패키지 및 모듈을 불러올 때, *을 사용하면 해당 모듈의 모든 식별자들을 불러온다.
- 패키지 자체를 import시에 자동으로 가져오고 싶은 목록이 있다면, 패키지의 __init__.py파일에 해당 항목을 import해주면 된다.
- 특정 디렉터리의 모듈을 ```*```를 이용하여 import할 때에는 다음과 같이 해당 디렉터리의 ```__init__.py 파일```에 ```__all__```이라는 변수를 설정하고 import할 수 있는 모듈을 정의해 주어야 한다.
```python
# C:/Python/game/sound/__init__.py
__all__ = ['echo']
```
- 여기서 ```__all__```이 의미하는 것은 sound 디렉터리에서 ```*``` 기호를 이용하여 import할 경우 ```이곳에 정의된 echo 모듈만 import```된다는 의미이다.

### 패키지 안의 함수 실행하기
- 패키지 기본 구성
```python
C:/Python/game/__init__.py
C:/Python/game/sound/__init__.py
C:/Python/game/sound/echo.py
C:/Python/game/graphic/__init__.py
C:/Python/game/graphic/render.py
```
- echo.py 파일은 다음과 같이 만든다.
```python
# echo.py
def echo_test():
    print ("echo")
```
- 첫 번째는 ```echo 모듈을 import```하여 실행하는 방법으로, 다음과 같이 실행한다
```python
>>> import game.sound.echo
>>> game.sound.echo.echo_test()
echo
```
- 두 번째는 ```echo 모듈이 있는 디렉터리까지를 from ... import```하여 실행하는 방법이다.
```python
>>> from game.sound import echo
>>> echo.echo_test()
echo
```
- 세 번째는 ```echo 모듈의 echo_test 함수를 직접 import```하여 실행하는 방법이다.
```python
>>> from game.sound.echo import echo_test
>>> echo_test()
echo
```
- 하지만 다음과 같이 echo_test 함수를 사용하는 것은 불가능하다.
```python
>>> import game
>>> game.sound.echo.echo_test()
Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
AttributeError: 'module' object has no attribute 'sound'
```
- 또 다음처럼 echo_test 함수를 사용하는 것도 불가능하다.
```python
>>> import game.sound.echo.echo_test
Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
ImportError: No module named echo_test
```
- 도트 연산자(.)를 사용해서 import a.b.c처럼 import할 때 ```가장 마지막 항목인 c```는 **반드시** ```모듈 또는 패키지```여야만 한다.
- <https://wikidocs.net/1418>

##실습
1. 위 프로그램에 friends패키지를 만들고, send_message함수를 가진 chat모듈을 추가한다.
send_message는 input을 이용해 2개의 인자를 받으며(친구명, 메세지), 실행 시 print함수를 통해 메세지를 보냈다는 문구를 출력한다.
2. 프로그램을 실행했을 때, 3을 입력하면 send_message함수를 실행하도록 한다.

3. 커맨드라인으로 인자를 전달받아, 모두 더한 결과를 출력하는 모듈을 만든다. 이 때, 인터프리터를 통해 실행되었을 때만 결과가 출력되도록 한다.

4. 위 3번의 프로그램에서, 정수형 데이터로 변환할 수없는 인자값이 올 경우 '올바른 값이 주어지지 않았습니다' 를 출력하며 종료되도록 프로그램을 리펙토링해본다. 내장함수 isintance를 사용한다.
```

```