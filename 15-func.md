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

-  change_global_champion함수에서 오류가 발생하는 이유.
```
UnboundLocalError: local variable 'champion' referenced before assignment
```
- 내부에 또 다른 ```champion = 'aHri' 변수```가 존재하기 때문에 할당하기 전인 변수를 사용한 것으로 판단하여 프로그램에서 오류를 발생시킨다.
- 안쪽(Local)에서는 바깥 영역(Global)의 변수를 참조할 수 있으나,
- 바깥쪽에서는 안쪽 영역의 변수를 참조할 수 없다.
- 이름이 같은 두 변수가 다른 객체임을 내장함수 id를 사용해 확인해보자.
- 각 영역에 해당하는 데이터들은 ```locals()함수```를 사용해 확인 할 수 있으며, 전역 영역의 데이터들은 ```globals()함수```를 사용한다.

### 스코핑 룰
- local, global, built-in 영역이 존재.
- Built-in 영역이 가장 바깥, 그 내부에 global, 그 global 영역 안에 local로 정의된다.
- 외부 영역에서는 내부 영역의 데이터를 사용할 수 없지만 내부 영역에서는 자신의 외부 영역에 있는 데이터를 참조할 수 있다.
- 반대의 경우에는 함수의 인자로 데이터를 전달한다.

### 내장함수와 내장 영역
 - \_\_builtin\_\_ 변수
 - dir 함수
 	- 해당 객체가 사용 가능한 속성 및 함수들을 리스트 형태로 나타내준다.
 
### local scope에서  global scope의 변수 사용
```python
In [13]: def change_global_champion():
    ...:     global champion
    ...:     champion = 'aHri'
    ...:     print('after change_global_champion: {}'.format(champion))
    ...:     print('locals()'.format(locals()))
    ...: 
In [14]: change_global_champion()
after change_global_champion: aHri
```
- 만약 로컬 스코프에서 글로벌 스코프의 변수를 변경해야 한다면, 해당 변수가 로컬 스코프에 생성되는 것이 아닌 글로벌 영역에 이미 존재하는 값을 사용함을 명시해주어야 한다.

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
- 로컬 스코프 내부에는 또 다른 로컬 스코프가 존재할 수 있다.
- 전역 스코프가 아닌, 자신의 바로 바깥 영역의 로컬 스코프(자신보다 한 단계 위의 로컬 스코프)의 데이터를 참조하고자 한다면, ```nonlocal```키워드를 사용한다.
- nonlocal 키워드는 위를 타고 간다.
```python
  1 champion = 'Lux'
  2
  3 def local1():
  4     champion = 'Ahri'
  5     print('local1 locals() : {}'.format(locals()))
  6     # 여기서는 Ahri가 출력
  7     print(champion)
  8 
  9     def local2():
 10         nonlocal champion
 11         champion = 'Ezreal'
 12         print('local2 locals() : {}'.format(locals()))
 13         # 여기서는 Ahri가 Ezreal로 변경되어서 출력(nonlocal로 선언했기에)
 14         print(champion)
 15 
 16     local2()
 17     print('after local2(), local1 locals(): {}'.format(locals()))
 18     # 여기서는 Ahri가 Ezreal로 변경되어서 출력
 19     print(champion)
 20 
 21 #print('global locals() : {}'.format(locals()))
 22 local1()
 23 # 여기서는 global 변수이므로, Lux가 출력
 24 print(champion)
```

### global 인자와 argument(인자) 전달의 차이
- 실습(diff_global_arg.py)
- 결과
```python
global_level = 100

def arg_level_add(value):
    value += 30
    print('arg_level_add, value : %s' % value)
 
def global_level_add():
    global global_level
    global_level += 30
    print('global_level_add, global_value : %s' % global_level)

def show_global_level():
    print('global_level : %s' % global_level)

show_global_level()
arg_level_add(global_level)
show_global_level()
global_level_add()
show_global_level()

global_level : 100
arg_level_add, value : 130
global_level : 100
global_level_add, global_value : 130
global_level : 130
```
- ```인자```로 전달하였기 때문에, ```매개변수인 value의 값```을 변경하는 것은 ```전역 변수인 global_level```에는 영향을 주지 않는다.
 - 리스트로 변경 후, 결과
```python
global_level = [100]

def arg_level_add(value):
    value[0] += 30
    print('arg_level_add, value : %s' % value)
 
def global_level_add():
    global global_level
    global_level[0] += 30
    print('global_level_add, global_value : %s' % global_level)

def show_global_level():
    print('global_level : %s' % global_level)

show_global_level()
arg_level_add(global_level)
show_global_level()
global_level_add()
show_global_level()

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
- ```함수의 전역 영역은 해당 함수가 정의된 모듈의 전역 영역```으로, ```전역변수```는 ```모듈의 영역에 영향```을 받는다.

#### 내부함수의 closure
```python
  1 level = 0
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
 24 
 25 def inner():
 26     global level
 27     level+=3
 28     print(level)
 29 
 30 inner()
 31 inner()
 32 inner()
```
- outter함수는 inner함수를 반환하여 결과를 func전역변수에 할당한다.
- inner함수의 호출 결과가 아닌 ```함수 자체를 반환```하기 때문에, func변수는 실행할 수 있는 ```함수객체```
- inner함수가 사용하는 level변수는 ```nonlocal키워드```를 사용했기 때문에 ```outter에 새로 정의된 지역변수 level```을 사용한다.

```python
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
 - 반복적으로 func함수를 실행하면 inner의 외부(outter)에 존재하는 level변수의 값을 증가시키고 print시키기 때문에, 값은 계속해서 증가한다.
 - func 는 outter 함수를 통해 inner 함수에 있는 영역까지를 반환 받았다. inner 함수가 return 됐으니까.
 - closure 영역을 이해시키기 위한 예제
 - inner 함수에서
```python
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
```python
  3     level = 50
  4 
  5     def inner():
  6         nonlocal level
  7         level += 3
  8         print(level)
```
- ```nonlocal키워드```를 사용했기 때문에, closure 영역은 3 Line도 포함.(3 ~8 Line 까지)

### 데코레이터(decorator)
- 함수를 받아 다른 함수를 반환하는 함수
- 기존에 존재하던 함수를 바꾸지 않고 전달된 인자를 보기위한 디버깅 print함수를 추가한다던가 하는 기능을 추가할 수 있다.
	1. 기능을 추가할 함수를 인자로 받음
	2. 데코레이터 자체에 추가할 기능을 함수로 정의
	3. 인자로 받은 함수를 데코레이터 내부에서 적절히 호출
	4. 위 2가지를 행하는 내부 함수를 반환
- 데코레이터를 사용할 경우에는 함수 위에 ```데코레이터```를 **추가**해서 사용가능하다.
```
함수를 실행할 때, ```로그를 남길 때```, 주로 **decorator 함수**를 사용
```
```python
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
- yield부분에서 멈춘 제네레이터 객체를 순회하기 위해서는 __next__() 함수를 실행해준다.
- 함수를 통해서 만들어지며, 함수 내부의 반복문에서 ```yield```키워드를 사용하면 제네레이터가 된다.
- list 가 100만개 있으면, 100만개 전부 메모리를 써야 되지만,
generator에서는 for, while 구간 만큼의 메모리만 차지하므로, 메모리를 save 할 수 있다.
```python
def generator(n):
    i = 0
    while i < n:
        yield i
        i += 1

for x in generator(5):
print x

0
1
2
3
4 
```
```
1. for 문이 실행되며, 먼저 generator 함수가 호출된다.
2. generator 함수는 일반 함수와 동일한 절차로 실행된다. 
3. 실행 중 while 문 안에서 yield 를 만나게 된다. 그러면 return 과 비슷하게 함수를 호출했던 구문으로 반환하게 된다. 여기서는 첫번재 i 값인 0 을 반환하게 된다. 하지만 반환 하였다고 generator 함수가 종료되는 것이 아니라 그대로 유지한 상태이다.
4. x 값에는 yield 에서 전달 된 0 값이 저장된 후 print 된다. 그 후 for 문에 의해 다시 generator 함수가 호출된다. 
5. 이때는 generator 함수가 처음부터 시작되는게 아니라 yield 이후 구문부터 시작되게 된다. 따라서 i += 1 구문이 실행되고 i 값은 1로 증가한다.
6. 아직 while 문 내부이기 때문에 yield 구문을 만나 i 값인 1이 전달 된다.
7. x 값은 1을 전달 받고 print 된다. (이후 반복)
출처: http://bluese05.tistory.com/56
```
### 실습
1. 매개변수로 문자열을 받고, 해당 문자열이 red면 apple을, yellow면 banana를, green이면 melon을, 어떤 경우도 아닐 경우 I don't know를 리턴하는 함수를 정의하고, 사용하여 result변수에 결과를 할당하고 print해본다.
2. 1번에서 작성한 함수에 docstring을 작성하여 함수에 대한 설명을 달아보고, help(함수명)으로 해당 설명을 출력해본다.
```python
 def print_fruits(string):
 25     """return apple if argument is red \n
 26     return banana if argument is yellow \n
 27     return melon if argument is green \n
 28     return I don\'t know if argument doesn\'t match"""
 29     if(string == 'red'):
 30         return 'apple'
 31     elif (string == 'yellow'):
 32         return 'banana'
 33     elif (string == 'green'):
 34         return 'melon'
 35     else :
 36         return ('I don\'t know')
 37 
 38 
 39 string = input("문자열을 입력하세요: ")
 40 result = print_fruits(string)
 41 print(result)
 42 
 43 print("문제 2")
 44 help(print_fruits)
```

3. 한 개 또는 두 개의 숫자 인자를 전달받아, 하나가 오면 제곱, 두개를 받으면 두 수의 곱을 반환해주는 함수를 정의하고 사용해본다.
```python
# 갯수가 안정해져 있을 경우
def multiply_or_square(*args):
        if(len(args) == 1):
            print('숫자 {}, 1개 입력'.format(args[0]))
            c = args[0]**2
            return c
        if(len(args) == 2):
            print('숫자 {}와 {}, 2개 입력'.format(args[0], args[1]))
            c = args[0] * args[1]
            return c
        else: 
            print("I don\'t know")
    
result = multiply_or_square( 2, 7)
print(result)
result = multiply_or_square( 7)
print(result)
# 갯수가 안정해져 있을 경우

# 강사 : 갯수가 정해져 있을 경우
def sqaure_or_multi(arg1, arg2 = None):
    if arg2 is None:
        print(arg1 * arg1)
    else :
        print(arg1 * arg2)
# 갯수가 정해져 있을 경우
```
4. 두 개의 숫자를 인자로 받아 합과 차를 튜플을 이용해 동시에 반환하는 함수를 정의하고 사용해본다.
```python
def return_sum_sub(arg1, arg2):
 	print(arg1+arg2, arg1-arg2 if arg1 > arg2 else arg2 - arg1)
 return_sum_sub(3,5)
```
5. 위치인자 묶음을 매개변수로 가지며, 위치인자가 몇 개 전달되었는지를 print하고 개수를 리턴해주는 함수를 정의하고 사용해본다.
```python
111 def print_args_info(*args, **kwargs):
112     args_count = len(args)
113     print('args count : {}'.format(args_count))
114     return args_count
115 
116 result = print_args_info(3,5,10,'asdf',[])
117 print(result)
```
6. 람다함수와 리스트 컴프리헨션을 사용해 한 줄로 구구단의 결과를 갖는 리스트를 생성해본다.
```python
def make_gugu():
    ret = []
    for i in range(2,10):
        for j in range(1,10):
            ret.append('{} x {} = {}'.format(i,j,i*j))
    return ret 

result == make_gugu()
result_str = '\n'.join(result)
print(result_str)

def make_gugu2()
    # for 문 먼저 list comprehension 으로 구현
    return [(x,y) for x in range(2,10) for y in range(1,10)] 
result = make_gugu2()
result_str = '\n'.join(result)
print(result_str)

def make_gugu3()
    # 그 다음 lambda 함수 구현
    return [ (lambda a, b : '{} x {} = {}'.format(a, b, a*b))(x,y) for x in range(2,10) for y in range(1,10)] 

result = make_gugu3()
result_str = '\n'.join(result)
print(result_str)
```
### 알고리즘
1. 순차검색(Sequential Search)
	- 문자열과 키 문자 1개를 받는 함수 구현
	- while문을 이용, 문자열에서 키 문자가 존재하는 index위치를 검사 후 해당 index를 리턴
	- 찾지 못했을 경우 0을 리턴
```python
def search(key, source):
    length = len(source)
    index = 0 
    while index < length :
        cur_char = source[index]
        if cur_char == key :
            return index
        index+=1
    return 0

def search2(key, source):
    # enumerate는 순서가 있는 자료형(리스트, 튜플, 문자열)을 입력으로 받아 인덱스 값을 포함하는 enumerate 객체를 리턴한다.
    for index, char in enumerate(source):
        if char == key :
            return index
    return 0

source = 'Lux, the lady of luminosity'
result = search('o', source)
print(result)
result = search2('o', source)
print(result)
```

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
```python
DEBUG = True
source = [9, 1, 6, 8, 4, 3, 2, 0, 7, 5]
length = len(source)
def select_sort():
    # 1. 일단 (n-1)번째 문자열을 순환
    # 마지막 문자는 앞의 문자들이 오름차순으로 정렬되므로 정렬이 필요없다.
    for index in range(length-1):
        cur_min_index = index # 4.
        if DEBUG :
            print(index)
            print('index {} loop, cur value : {}'.format(index, source[index]))
        #for inner_index in range(length): # 2 

        # 비교하려는 문자 다음부분부터 순회한다.
        for inner_index in range(index+1, length): # 3
            if DEBUG : 
                print(' inner index {} loop, cur value : {}'.format(inner_index, source[inner_index]))
        # 3. 디버깅 메제지를 보면서 알고리즘을 완성한다.
            
                print(' min_value : {}, cur_value: {}'.format(source[cur_min_index], source[inner_index])) #4
            # 만약 현재 값이 cur_min_index의 값보다 작을 경우    
            # 해당 index 값이(inner index)를 cur_min_index에 기록한다.
            # 5
            if source[cur_min_index] > source[inner_index] :
                cur_min_index = inner_index
                if DEBUG :
                    print(' change min val({}), index : {}'.format( source[cur_min_index], source[inner_index]))
        # 6 
        if cur_min_index != index :
            source[cur_min_index], source[index] =  source[index], source[cur_min_index]

select_sort()
# 알고리즘은 짜면서 디버깅 메세지를 통해 확인해가면서 완성해 간다.
```


