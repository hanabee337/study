# 제어문(if, for, while, comprehension)

### if 문
#### 한줄 표현식
```
vacation = 7
print('good') if vacation >= 7 else print('bad') if(vacation >=5) else print('soso')
```

### for 문
- iterable한 객체에는 문자열, 튜플, 딕셔너리, 셋 등이 있다.
- 딕셔너리에서 키나 값을 순회할 때는, iterable한 객체의 위치에 dict.keys()나 dict.values()를 사용한다.
- 키, 값을 모두 순회할 때에는 dict.items()를 사용한다.
```
In [5]: for i in range(2,10,1):
   ...:	print('{}단'.format(i))
   ...:     for j in range(2,10,1):
   ...:         print("{} X {} = {}".format(i,j,i*j))
   ...:     print("\n")
```
#### break
특정 조건에서 반복을 멈추고 조건문을 빠져나갈때, 사용.

#### continue
다음 반복문으로 건너뛸 때, 사용.

#### break확인 (else)
```
for 항목 in iterable객체:
  pass
else:
  for문으로 진입하지 않았거나, for 문에서 break문이 호출되지 않았을 떄, 사용.
```
### 여러 시퀀스 동시순회(zip)
zip을 사용하면 여러 시퀀스로부터 튜플을 만들 수 있다.

```
In [32]: colors = ['red', 'green', 'yellow']
In [34]: fruits = ['apple', 'melon', 'banana']
In [35]: for item in zip(fruits, colors):
    ...:     print(item)
    ...:     print(type(item))
    ...:     
('apple', 'red')
<class 'tuple'>
('melon', 'green')
<class 'tuple'>
('banana', 'yellow')
<class 'tuple'>
```

```
In [36]: result = zip(colors, fruits)
In [37]: print(type(zip))
<class 'type'>
In [38]: print(type(result))
<class 'zip'>
```
```
In [40]: result_list = list(result)
In [41]: result_list
Out[41]: [('red', 'apple'), ('green', 'melon'), ('yellow', 'banana')]
```
### while
- for문과 유사하나, while뒤의 조건이 참일 경우에 계속해서 반복한다.

### Comprehension
1. List Comprehension

```
[표현식 for 항목 in iterable객체]
예) [item for item in range(1, 6)]
[1, 2, 3, 4, 5]

In [43]: [item for item in range(1,6)]
Out[43]: [1, 2, 3, 4, 5]

In [44]: [item*2 for item in range(1,6)]
Out[44]: [2, 4, 6, 8, 10]

In [45]: [if(item%2==0) for item in range(1,6)]
  File "<ipython-input-45-d7cd1f7b771a>", line 1
    [if(item%2==0) for item in range(1,6)]
      ^
SyntaxError: invalid syntax


In [46]: [for item in range(1,6) if(item%2==0)]
  File "<ipython-input-46-091e542be441>", line 1
    [for item in range(1,6) if(item%2==0)]
       ^
SyntaxError: invalid syntax


In [47]: [item for item in range(1,6) if(item%2==0)]
Out[47]: [2, 4]
```

2. Set Comprehension

```
In [4]: g= (item for item in range(10))

In [5]: g
Out[5]: <generator object <genexpr> at 0x7f1be61de558>

In [6]: for i in (g)
  File "<ipython-input-6-15ead12d54ee>", line 1
    for i in (g)
                ^
SyntaxError: invalid syntax


In [7]: for i in (g):
   ...:     print(i)
   ...:     
0
1
2
3
4
5
6
7
8
9
```

3. Generator Comprehension

#### 실습

1. for문을 2개 중첩하여 (0,0), (0,1), (0,2), (0,3), (1,0), (1,1)..... (6,3)까지 출력되는 반복문을 구현한다.  

```
In [8]: for i in range(0,7,1):
   ...:     for j in range(0,4,1):
   ...:         print('({},{})'.format(i,j))
   ...:
```  
2. 리스트 컴프리헨션을 중첩하여 위 결과를 똑같이 출력한다.
```
In [12]: [(i,j) for i in range(0,7,1) for j in range(0,4,1)]
```
3. 1, 2번의 반복문에서 튜플의 첫 번째 항목이 짝수일때만 출력하도록 조건을 변경한다.
```
In [31]: for i in range(2,10):
    ...:     if(i%2!=0):
    ...:         continue
    ...:     for j in range(2,10,1):
    ...:         print('({}, {})'.format(i,j))
In [32]: [(i,j) for i in range(7) if i%2 == 0 for j in range(4)]
```
4. 1000에서 2000까지의 숫자 중, 홀수의 합을 구해본다.
```
i=1000
sum=0
In [22]: while(i<=2000):
    ...:     	if(i%2==1):
    ...:      		sum+=i;
    ...:     	i+=1;
    ...: 	print(sum)
```
5. 리스트 컴프리헨션을 사용하여 구구단 결과를 갖는 리스트를 만들고,  
 해당 리스트를 for문을 사용해 구구단 형태로 나오도록 출력해본다.
각 단마다 한 번 더 줄바꿈을 넣어준다.
```
  case 1
OK : ['{} X {} = {}'.format(i,j,i*j) for i in range(2,10) for j in range(2,10)]
이렇게 하면 정상적인데,
print문을 추가하면 이상하게 나옴. 구구단이 다 출력되고 나서도 None이 출력됨. why?
NG:  [print('{} x {} = {}'.format(i,j,i*j)) for i in range(2,10) for j in range(2,10)]

  case 2
In [40]: result_list = [i*j for i in range(2,10) for j in range(2,10)]
In [41]: index = 0
In [42]: for i in range(2,10):
    ...:     for j in range(2,10):
    ...:         print('{} x {} = {}'.format(i,j,result_list[index]))
    ...:         index+=1
```

6. 1에서 99까지의 정수 중, 7의 배수이거나 9의 배수인 정수인 리스트를 생성한다.
 단, 7의 배수이며 9의 배수인 수는 한 번만 추가되어야 한다.
```
In [34]: com_list = []
In [35]: for i in range(1,100):
    ...:     if(i%7==0 or i%9==0):
    ...:         com_list.append(i)
    ...:
In [36]: print(com_list)
[7, 9, 14, 18, 21, 27, 28, 35, 36, 42, 45, 49, 54, 56, 63, 70, 72, 77, 81, 84, 90, 91, 98, 99]
In [38]: print(list(set(com_list)))
```

### enumerate
- iterate 하는 횟수를 알고 싶을 때, 사용
```
In [34]: for index, x in enumerate(range(1002,1010)):
    ...:     print('index: {}, value :{}'.format(index, x))
    ...:     
index: 0, value :1002
index: 1, value :1003
index: 2, value :1004
index: 3, value :1005
index: 4, value :1006
index: 5, value :1007
index: 6, value :1008
index: 7, value :1009
```

# 함수
- 반복적인 작업을 미리 정의해 놓은 것.
```
In [35]: def func():
    ...:     for i in range(2,10):
    ...:         print('call func')
    ...: 
In [36]: func
Out[36]: <function __main__.func>
```
<span color=red>__main__</span> 의미는 module


### 함수 실행
### 매개변수와 인자의 차이
```
함수 내부에서 함수에게 전달되어 온 변수는 매개변수라 부르며,
함수를 호출할 때 전달하는 변수는 인자로 부른다.
```
~~~
# 함수 정의 때는 매개변수
def func(매개변수1, 매개변수2):
  ...
# 함수 호출 시에는 인자
>>> func(인자1, 인자2)
~~~

### None 객체
- 함수에서 return 값이 없을 경우, 아무것도 없다는 뜻의 ```None``` 객체를 가짐.

### 위치 인자
- 매개변수의 순서대로 반드시 인자를 전달하여 사용해야만 하는 경우  
```
In [51]: def get_student(name, age, gender):
    ...:     new_student = {
    ...:     'name' : name,
    ...:     'age' : age,
    ...:     'gender' : gender
    ...:     }
    ...:     return new_student
    ...:
In [53]: get_student('hanyeong.lee', 30, 'male')
Out[53]: {'age': 30, 'gender': 'male', 'name': 'hanyeong.lee'}
```

### 키워드 인자
- 매개변수의 이름을 지정하여 인자로 전달하여 사용하는 경우.
- 키워드로 받을 인자는 가장 맨 뒤에 와야 함.
- 위치인자와 키워드인자를 동시에 쓴다면, 위치인자가 먼저 와야 한다.
```
In [54]: get_student(age=30,gender ='male', name='Kim')
Out[54]: {'age': 30, 'gender': 'male', 'name': 'Kim'}
result = get_student(age=30,gender ='male', name='Kim'
print(type(result))
<class 'dict'>
```
### 기본 매개변수 값의 정의 시점
>	기본 매개변수값은 함수가 실행될 때 마다 계산되지 않고,  
	함수가 정의되는 시점에 계산되어 계속해서 사용된다.  

```
In [61]: def return_list(val, result=[]):
    ...:     if result is None:
    ...:         result = []
    ...:     result.append(val)
    ...:     return result
    ...:
In [62]: return_list('apple')
Out[62]: ['apple']

In [63]: frutis_list = ['banana', 'apple']
In [64]: return_list(frutis_list)
Out[64]: ['apple', ['banana', 'apple']]
```

```
In [87]: def return_list2(val, result=None):
    ...:     if result is None:
    ...:         result = []
    ...:     result.append(val)
    ...:     return result
    ...:

In [88]: fruits_list = 'banana'
In [89]: result = return_list2(fruits_list)
In [90]: result
Out[90]: ['banana']

In [91]: fruits_list = 'melon'
In [92]: result = return_list2(fruits_list)
In [93]: result
Out[93]: ['melon']
```

### 위치인자 묶음(*)
- 함수에 위치인자로 주어진 변수들의 묶음은 ```매개변수명```으로 사용할 수 있다.
- ```tuple 형식으로 return```
```
def print_args(*args):
  print(args)
```

```
In [43]: def print_arg(*arg):
...:     print(arg)
...:

In [44]: print_arg(1,2,'abc')
(1, 2, 'abc')
In [46]: print_arg(1,2,'abc', 34,'kim')
(1, 2, 'abc', 34, 'kim')
In [47]: result = print_arg(1,2,'abc', 34,'kim')
(1, 2, 'abc', 34, 'kim')

In [48]: print(type(result))
<class 'NoneType'>
```

### 키워드 인자 묶음
- 함수에 키워드인자로 주어진 변수들의 묶음은 ```매개변수명```으로 사용할 수 있다
- ```dict 형식으로 return```

```
In [56]: def all_args(*args, **kwargs):
    ...:     print('positional arg:', args)
    ...:     print('keyword args: ', kwargs)
    ...: 
 In [57]: all_args('one','two','three')
positional arg: ('one', 'two', 'three')
keyword args:  {}

In [58]: all_args(a='one',b='two',c='three')
positional arg: ()
keyword args:  {'c': 'three', 'a': 'one', 'b': 'two'}

In [59]: all_args('one','two',c='three', d='four')
positional arg: ('one', 'two')
keyword args:  {'c': 'three', 'd': 'four'}

In [63]: def print_kwargs(**kwargs):
    ...:     print('kwargs count {}'.format(len(kwargs)
    ...: ))
In [64]: print_kwargs(a='abc', b='def')
kwargs count 2
```
### docstring
```
In [62]: def print_args(*args):
    ...:     'Print Positional arguments and return argument count'
    ...:     print(args)
    ...:     return len(args)
```
```
In [63]: help(print_args)

Help on function print_args in module __main__:
print_args(*args)
    Print Positional arguments and return argument count
(END)
```

### 함수를 인자로 전달
- 파이썬에선 ```함수도 객체```로 인식하기 때문에 함수로 인자 전달이 가능하다.
```
def call_func():
	print('call func')

def excute_call_func(func):
	func()

execute_call_func(call_func)
```

### 내부 함수
- 함수 안에서 또 다른 함수를 정의해 사용할 수 있다.
```
In [107]: def outer(val):
     ...:     def inner(string):
     ...:         return string.upper()
     ...:     return inner(val)
     ...:
In [109]: outer("test")
Out[109]: 'TEST'

In [115]: def outer2(val):
     ...:     	def inner2(string):
     ...:         	return string.upper()
     ...:     return inner2(val)
     ...:
In [116]: outer2('test')
Out[116]: 'TEST'
```

### 로컬 스코프에서 글로벌 스코프

### global키워드와 인자(argument)전달의 차이

### lamda 함수
