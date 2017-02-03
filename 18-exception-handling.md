# 예외 처리
- 오류가 발생하면 프로그램은 에러를 출력하며 강제종료되거나,
 원하지 않는 동작을 한다.
- 이러한 오류를 안전하게 처리하고, 바로 강제종료 되지 않고,
 오류 발생 후 처리할 루틴을 실행하고자 할 때, 예외처리를 사용한다.
### 기본 형태
```python
try:
    시도할 코드
except:
    에러가 발생했을 경우 실행할 코드
```
```python
In [1]: sample_list = ['apple', 'banana', 'melon']

In [2]: try:
   ...:     print(sample_list[4])
   ...: except:
   ...:     print('Out of list range')
   ...: 
Out of list range
```

### 여러가지 예외를 구분할 경우
```python
try:
    시도할 코드
except <예외 클래스1>:
    에러클래스 1에 해당할 때 실행할 코드
except <예외 클래스2>:
    ...
except <예외 클래스3>:
    ...
```
```python
In [3]: sample_list = ['apple', 'banana', 'melon']
In [4]: sample_dict = { 
   ...:         'game' : ['lol', 'startcraft'],
   ...:         'food' : ['hamburger', 'pizza'],
   ...:         'color' : ['red', 'yellow', 'green']
   ...:         }
   ...: try :
   ...:     print(sample_list[2])
   ...:     print(sample_dict['fruits'])
   ...: except IndexError:
   ...:     print('리스트 인덱스 범위 넘었음')
   ...: except KeyError:
   ...:     print('딕 키가 없음')
   ...: 
melon
딕 키가 없음
```

### 예외사항을 변수로 사용할 경우
```python
try:
    시도할 코드
except <예외클래스> as <변수명>:
    <변수명>을 사용한 코드
```
```python
 In [5]: try :
   ...:     print(sample_list[2])
   ...:     print(sample_dict['fruits'])
   ...: except IndexError as e:
   ...:     print(e)
   ...: except KeyError as e:
   ...:     print(e)
   ...: 
melon
'fruits'
```
### try ~ else
- ```else문```은 try이후 예외가 발생하지 않을 경우 실행된다.
```python
try:
    시도할 코드
except:
    예외 발생시 실행 코드
else:
    예외가 발생하지 않았을 시 실행할 코드
```
- 하기 코드 참조

### try ~ finally
- ```finally문```은 try이후 예외가 발생하건, 하지않건 무조건 마지막에 실행된다.
- 하기 코드 참조

### 예외 발생시키기(raise)
- 예외를 발생시킬때는 raise구문을 사용한다.
- 하기 코드 참조

### 실습
- 예외 만들기
	- 내장 클래스 Exception을 상속받아 커스텀 예외를 만들 수 있다.
	- 초기화 메서드에서 예외에서 처리할 데이터를 받고,
	print문으로 사용되고 싶다면 \_\_str\_\_메서드를 오버라이드 해준다.
	- projects/python/except/custom_exception.py 참조
	
```python
import re

class NotMatchedException(Exception) :
    # 에외 자체(NotMatchedException 함수)에다가 어디를 찾다가 에러가 발생했다는 정보를 전달
    
    def __init__(self, re_pattern=None, source=None) :
        # 정규표현식 compile된 객체를 찾을 수 있다
        # 만약 인자로 주어진 re_pattern 객체가
        # re._pattern.type형객체라면
        # (컴파일된 정규표현식 패턴 객체)
        # self.pattern_str 속성에 re_pattern.pattern값을 할당
        if isinstance(re_pattern, re._pattern_type):
            self.pattern_str = re_pattern.pattern

        # re_pattern 객체가 str(문자열)형일 경우
        # self.pattern_str 속성에 해당 값을 그대로 할당
        elif isinstance(re_pattern, str) :
            self.pattern_str = re_pattern

        self.source = source

    def __str__(self):
        return 'Pattern ({}) is not matched in source({})'.format(self.pattern_str, self.source)

def search_from_source(pattern, source):
    m = re.search(pattern, source)
    if m :
        return m
    else :
        raise NotMatchedException(pattern, source)

try :
    print('--try search_from_source--')
    source = 'Lux, the Lady of Luminosity'
    # 매칭되지 않는 str
    pattern_str1 = 'Ladyyyy'
    # 매칭되는 str
    pattern_str2 = r'\w+\s+Lady\s+\w+'
    pattern = re.compile(pattern_str1)		-------------> (1)
    #pattern = re.compile(pattern_str2) 	-------------> (2)
    print(type(pattern))
    m = search_from_source(pattern, source)
    
except NotMatchedException as e:
    print(e)
else :
    print(' result : {}'.format(m.group()))
finally :
    print('--end search_from_source--')

print('----Program Terminate-----')
```
- (1)의 결과
```python
$ python custom_exception.py
--try search_from_source--
<class '_sre.SRE_Pattern'>
Pattern (Ladyyyy) is not matched in source(Lux, the Lady of Luminosity)
--end search_from_source--
----Program Terminate-----
```
- (2)의 결과
```python
$ python custom_exception.py
--try search_from_source--
<class '_sre.SRE_Pattern'>
 result : the Lady of
--end search_from_source--
----Program Terminate-----
```