# Module
### module
- 지금까지 shell에서 진행한 실습의 경우, 하나의 모듈 내부에서 작업한 것으로 취급된다.
- python 파일은 각각 하나의 module로 취급된다.

### import 실습
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

### from 을 사용해 module의 함수를 직접 import
- ```import 모듈명```의 경우, 모듈의 이름이 전역 네임스페이스에 등록되어 ```모듈명.함수```로 사용가능하다.
- 모듈명을 생략하고 모듈 내부의 함수를 쓰고 싶다면, ```from 모듈명 import 함수명```으로 불러들일 수 있다.
### from module명 *을 사용해 module 내 모든 식별자(함수,변수) import
- ```from 모듈명 import``` 또는 ```import 모듈명```에서, 같은 모듈명이 존재하거나 혼동 될 수 있을 경우, 뒤에 ```as```를 붙여 사용할 모듈명을 변경할 수 있다.


# Package
- **패키지**는 ```모듈들을 모아 둔 특별한 폴더```를 뜻한다.
- 폴더를 패키지로 만들면 ```계층 구조를 가질 수 있으며, 모듈들을 해당 패키지에 모을 수 있는 역할```을 한다.
- 패키지를 만들 때는 패키지로 사용할 폴더에 **\_\_init\_\_.py**파일을 넣어주면, 해당 폴더는 패키지로 취급된다. (비어있어도 무관하다)
- 패키지는 모듈과 동일하게 import할 수 있다.

### *, __all__
- 패키지에 포함된 하위 패키지 및 모듈을 불러올 때, *을 사용하면 해당 모듈의 모든 식별자들을 불러온다.
- 패키지 자체를 import시에 자동으로 가져오고 싶은 목록이 있다면, 패키지의 __init__.py파일에 해당 항목을 import해주면 된다.

##실습
1. 위 프로그램에 friends패키지를 만들고, send_message함수를 가진 chat모듈을 추가한다.
send_message는 input을 이용해 2개의 인자를 받으며(친구명, 메세지), 실행 시 print함수를 통해 메세지를 보냈다는 문구를 출력한다.
2. 프로그램을 실행했을 때, 3을 입력하면 send_message함수를 실행하도록 한다.

3. 커맨드라인으로 인자를 전달받아, 모두 더한 결과를 출력하는 모듈을 만든다. 이 때, 인터프리터를 통해 실행되었을 때만 결과가 출력되도록 한다.

4. 위 3번의 프로그램에서, 정수형 데이터로 변환할 수없는 인자값이 올 경우 '올바른 값이 주어지지 않았습니다' 를 출력하며 종료되도록 프로그램을 리펙토링해본다. 내장함수 isintance를 사용한다.
```

```