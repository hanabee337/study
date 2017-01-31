# 스코프(영역)
```python
In [1]: champion = 'Lux'

In [2]: def show_global_champion():
   ...:     print('show_global_champion:{}'.format(champion))
   ...:     

In [3]: show_global_champion()
show_global_champion:Lux

In [4]: print('print champion : {}'.format(champion))
print champion : Lux
```
```
In [2]: def change_global_champion():
   ...:     print('before change_global_champion: {}'.format(champion))
   ...:     champion = 'aHri'
   ...:     print('after change_global_champion: {}'.format(champion))
   ...:  
 In [4]: change_global_champion() 
```
```
UnboundLocalError: local variable 'champion' referenced before assignment
```
### 스코핑 룰
-  change_global_champion함수에서 오류가 발생하는 이유.
```
UnboundLocalError: local variable 'champion' referenced before assignment
```
 - 안쪽(Local)에서는 바깥 영역(Global)의 변수를 참조할 수 있으나,
 - 바깥쪽에서는 안쪽 영역의 변수를 참조할 수 없다.
 - 이름이 같은 두 변수가 다른 객체임을 내장함수 id를 사용해 확인해보자.
### 내장함수와 내장 영역
 - \_\_builtin\_\_ 변수
 
 - dir 함수
 	- 해당 객체가 사용 가능한 속성 및 함수들을 리스트 형태로 나타내준다.
 - 
 
### local 변수에서 global scope의 변수 사용
```
In [13]: def change_global_champion():
    ...:     global champion
    ...:     champion = 'aHri'
    ...:     print('after change_global_champion: {}'.format(champion))
    ...:     print('locals()'.format(locals()))
    ...: 
In [14]: change_global_champion()
after change_global_champion: aHri
```  
 
### 내부함수에서의 로컬 스코프(nonlocal)
 - 실습(nonlocal.py)
```
 global locals() : {'__doc__': None, '__loader__': <_frozen_importlib.SourceFileLoader object at 0x7f5f05624f28>, 'champion': 'Lux', '__builtins__': <module 'builtins' (built-in)>, '__name__': '__main__', '__cached__': None, '__spec__': None, '__file__': 'nonlocal.py', 'local1': <function local1 at 0x7f5f05656bf8>, '__package__': None}
local1 locals() : {'champion': 'Ahri'}
local2 locals() : {'champion': 'Ezreal'}
```
```
 nonlocal champion 추가
```
 - 실행 결과 
```
 global locals() : {'__cached__': None, '__spec__': None, '__loader__': <_frozen_importlib.SourceFileLoader object at 0x7f42adb6ef28>, '__name__': '__main__', '__builtins__': <module 'builtins' (built-in)>, '__package__': None, 'champion': 'Lux', 'local1': <function local1 at 0x7f42adba0bf8>, '__doc__': None, '__file__': 'nonlocal.py'}
local1 locals() : {'champion': 'Ahri'}
local2 locals() : {'champion': 'Ezreal'}
after local2(), local1 locals(): {'local2': <function local1.<locals>.local2 at 0x7f42adb4f268>, 'champion': 'Ezreal'}
```
- nonlocal 키워드는 위를 타고 간다.

### global 인자와 argument(인자) 전달의 차이
- 실습(diff_global_arg.py)
- 결과
```
global_level : 100
arg_level_add, value : 130
global_level : 100
global_level_add, global_value : 130
global_level : 130
```
 - 리스트로 변경 후, 결과
```
global_level : [100]
arg_level_add, value : [130]
global_level : [130]
global_level_add, global_value : [160]
global_level : [160]
```
- why?
- **list라서 변경되었다**. 같은 곳을 가리키므로...
- literal type이외는 모두 이와 같이 변경이 됨.

### Lambda 함수
```
lambda <매개변수> : <표현식>
```
-  함수 정의함과 동시에 실행이 가능.
-  반복문이나 조건문 등의 제어문은 포함될 수 없다.
```
# 함수의 정의
>>> def multi(x):
...   return x*x
... 

# 함수의 호출
>>> multi(5)
25

# 람다함수의 사용
>>> (lambda x : x*x)(5)
25

# 람다함수를 통한 함수 정의
>>> f = lambda x : x*x
>>> f(5)
25
```

### Closure
- modeul_a.py, module_b.py
- 어떤 함수가 실행되는 환경을 말한다.
- 함수가 정의된 영역
- 다른 모듈의 영역에 영향을 받지 않는 환경.
- 자신의 환경에 설정된 변수들만 사용함.
- 인자를 주고 받는 용도로 다른 모듈의 함수를 import해서 사용.
#### 내부함수의 closure
- outter함수는 inner함수를 반환하여 결과를 func전역변수에 할당한다.
- nner함수의 호출 결과가 아닌 함수 자체를 반환하기 때문에, func변수는 실행할 수 있는 함수객체
- inner함수가 사용하는 level변수는 nonlocal키워드를 사용했기 때문에 outter에 새로 정의된 지역변수 level을 사용한다.
```
  1 level = 0
  2 
  3 def outter():
  4     level = 50
  5 
  6     def inner():
  7         nonlocal level
  8         level += 3
  9         print(level)
 10     return inner
 11 
 12 func = outter()
 13 print(func)
 14 func()
 15 func()
```
- 결과 :
``` 
<function outter.<locals>.inner at 0x7f7fcbd7e268>
53
56
```
 - why?
 - func 는 outter 함수를 통해 inner 함수에 있는 영역까지를 반환 받았다. inner 함수가 return 됐으니까.
 - closure 영역을 이해시키기 위한 예제
 - inner 함수에서
```
  level = 0
  2 def outter():
  3     level = 50
  4     
  5     def inner():
  6         nonlocal level
  7         level += 3
  8         print(level)
  9     return inner
 10     
 11 func1 = outter()
 12 print('func1 id : %s' % id(func1))
 13 func1()
 14 func1()
 15 func1()
 16 print('')
 17 func2 = outter()
 18 func2() 
 19 func2()
 20 print('')
 21 print('func2 id : %s' % id(func2))
 22 print('func1 id : %s' % id(func1))
 23 print('')
 24 def inner():
 25     global level
 26     level+=3
 27     print(level)
 28 inner()
 29 inner()
 30 inner()
```
- 결과
```
func1 id : 140421968650856
53
56
59

53
56

func2 id : 140421968650992
func1 id : 140421968650856
3
6
9
```
-  closure 영역은 하기 부분
```
level = 50
  4     
  5     def inner():
  6         nonlocal level
  7         level += 3
  8         print(level)
```
### 데코레이터(decorator)
- 함수를 받아 다른 함수를 반환하는 함수
- 기존에 존재하던 함수를 바꾸지 않고 전달된 인자를 보기위한 디버깅 print함수를 추가한다던가 하는 기능을 추가할 수 있다.
	1. 기능을 추가할 함수를 인자로 받음
	2. 데코레이터 자체에 추가할 기능을 함수로 정의
	3. 인자로 받은 함수를 데코레이터 내부에서 적절히 호출
	4. 위 2가지를 행하는 내부 함수를 반환
- 데코레이터를 사용할 경우에는 함수 위에 ```데코레이터```를 **추가**해서 사용가능하다.
```
함수를 실행할 때, 로그를 남길 때, 주로 decorator 함수를 사용
```

```
  1 def print_args(func):
  2     def inner_func(*args, **kwargs):
  3         print('args : ', args)
  4         print('kwargs : ', kwargs)
  5         result = func(*args, **kwargs)
  6         return result
  7     return inner_func
 14 
 15 @print_args
 16 def multi(arg1, arg2):
 17 #    print('arg1 : {}, arg2: {}'.format(arg1, arg2))
 18     result =  arg1 * arg2
 19     print(result)
 20     return result
 21 
 22 @print_args
 23 def divide(arg1, arg2):
 24     # 똑같은 기능을 할 부분이 있음
 25 #    print('arg1 : {}, arg2: {}'.format(arg1, arg2))
 26     result = arg1 / arg2
 27     print(result)
 28     return result
 29 
 30 result1 = multi(3,5)
 31 result2 = divide(6,3)
```
- 실행 결과
```
args :  (3, 5)
kwargs :  {}
15
args :  (6, 3)
kwargs :  {}
2.0
```

### 제네레이터(generator)
- 제네레이터는 함수는 파이썬의 시퀀스 데이터를 생성하는데 사용된다
- 실제 시퀀스 데이터와 다른 점은, 시퀀스 전체를 가지고 있는 것이 아니라 시퀀스 데이터를 생성하기 위한 어떠한 루틴만을 가지고 있는 것이다
- 장점 : 전체 크기만큼의 메모리를 가지고 있는 시퀀스 데이터와는 달리 메모리를 적게 사용할 수 있다
-  마지막으로 호출한 위치(항목)에 을 기억하고 있으며, 한 번 순회할 때 마다 그 다음 값을 반환한다.
- 함수를 통해서 만들어지며, 함수 내부의 반복문에서 ```yield```키워드를 사용하면 제네레이터가 된다.
- list 가 100만개 있으면, 전부 메모리를 써야 되지만,
generator에서는 for, while 구간 만큼의 메모리만 차지하므로, 메모리를 save 할 수 있다.

### 실습
1. 매개변수로 문자열을 받고, 해당 문자열이 red면 apple을, yellow면 banana를, green이면 melon을, 어떤 경우도 아닐 경우 I don't know를 리턴하는 함수를 정의하고, 사용하여 result변수에 결과를 할당하고 print해본다.
```
```
2. 1번에서 작성한 함수에 docstring을 작성하여 함수에 대한 설명을 달아보고, help(함수명)으로 해당 설명을 출력해본다.
```
```
3. 한 개 또는 두 개의 숫자 인자를 전달받아, 하나가 오면 제곱, 두개를 받으면 두 수의 곱을 반환해주는 함수를 정의하고 사용해본다.
```
```
4. 두 개의 숫자를 인자로 받아 합과 차를 튜플을 이용해 동시에 반환하는 함수를 정의하고 사용해본다.
```
```
5. 위치인자 묶음을 매개변수로 가지며, 위치인자가 몇 개 전달되었는지를 print하고 개수를 리턴해주는 함수를 정의하고 사용해본다.
```
```
6. 람다함수와 리스트 컴프리헨션을 사용해 한 줄로 구구단의 결과를 갖는 리스트를 생성해본다.
```
```
### 알고리즘
1. 순차검색(Sequential Search)
	- 문자열과 키 문자 1개를 받는 함수 구현
	- while문을 이용, 문자열에서 키 문자가 존재하는 index위치를 검사 후 해당 index를 리턴
	- 찾지 못했을 경우 0을 리턴
2. 선택정렬(Selection sort)
	- [9, 1, 6, 8, 4, 3, 2, 0, 5, 7] 를 정렬한다.
	- 정렬과정
		- 리스트 중 최소값을 검색
		- 그 값을 맨 앞의 값과 교체
		- 나머지 리스트에서 위의 과정을 반복
	- 해결방법
		- 알고리즘 진행과정 그려보기
		- 의사코드(Psuedo code) 작성
		- 실제 코드 작성
```

```