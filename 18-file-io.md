# 파일 입출력

## 파일 열기(open)
```python
변수 = open(파일명, 모드)
```
- 모드의 첫 번째 글자

모드|설명
-|-
r|읽기
w|쓰기(파일이 이미 존재하는 경우, 덮어씀)
x|쓰기(파일이 존재하지 않을 경우에만)
a| 추가(파일이 존재할 경우 파일 끝부터 쓴다)

- 모드의 두 번째 글자

모드|설명
-|-
t 또는 없음| 텍스트 타입
b|바이너리 타입

### 파일 쓰기(write)
- skills.txt파일에 내용을 쓴다
```python
In [3]: skills = '''Illumination
   ...: ... Light Binding
   ...: ... Prismatic Barrier
   ...: ... Lucent Singularity
   ...: ... Final Spark'''
In [4]: len(skills)
Out[4]: 75

In [5]: f = open('skills.txt', 'wt')

In [6]: f.write(skills)
Out[6]: 75

In [7]: f.close()
```
- 만약 문자열이 클 경우, 일정 단위로 나누어서 파일에 쓰는 방식을 사용한다.
```python
In [10]: f = open('skills.txt', 'wt')
In [11]: size = len(skills)
In [12]: offset = 0
In [13]: chunk = 30
In [14]: while True :
    ...:     if offset > size :
    ...:         break
    ...:     f.write(skills[offset:offset+chunk])
    ...:     offset+=chunk
    ...: 

In [15]: skills
Out[15]: 'Illumination\nLight Binding\nPrismatic Barrier\nLucent Singularity\nFinal Spark'

In [16]: f.close()
```

### 파일 읽기(read)
- ```read()함수```는 **전체 파일을 한 번에** 가져오므로, **메모리 사용**에 유의해야한다.
```python
In [18]: f = open('skills.txt', 'rt')
In [19]: skills = f.read()
In [20]: f.close()
In [21]: len(skills)
Out[21]: 75

In [22]: print(skills)
Illumination
Light Binding
Prismatic Barrier
Lucent Singularity
Final Spark
```
- 한 번에 읽을 크기를 제한하고 싶다면, 인자로 최대 문자수를 입력해준다.
```python
>>> f = open('skills.txt', 'rt')
>>> chunk = 30
>>> while True:
...   part = f.read(chunk)
...   if not part:
...     break
...   skills += part
...
>>> f.close()
>>> len(skills)
75
```
- if not part :파일 끝에 도달하면 빈 문자열(' ')이 오는데,
빈 문자열은 if not part에서 False로 인식이 됨

### 텍스트파일 줄 단위 읽기(readline)
- readline()
- 파일 끝에 도달하면 빈 문자열(' ')이 오는데,
빈 문자열은 if not line에서 False로 인식이 됨
```python
In [1]: skills = ''
In [2]: f = open('skills.txt', 'rt')
In [3]: while True:
   ...:     line = f.readline()
   ...:     if not line:
   ...:         break
   ...:     skills+= line
   ...: 
In [4]: f.close()
In [5]: len(skills)
Out[5]: 75
```
### 이터레이터를 사용한 텍스트 파일 읽기
```python
In [7]: skills = ''
In [8]: f = open('skills.txt', 'rt')
In [9]: for line in f :
   ...:     skills += line
   ...: 
In [10]: f.close()
In [11]: len(skills)
Out[11]: 75
```
### 텍스트파일을 줄 단위 문자열 리스트로 리턴: readlines()
```python
In [12]: f = open('skills.txt', 'rt')
In [13]: lines = f.readlines()
In [14]: f.close()
In [15]: for line in lines :
    ...:     print(line)
    ...: 
Illumination

Light Binding

Prismatic Barrier

Lucent Singularity

Final Spark
```
- 각 줄에 줄바꿈(\n)문자가 있으므로, 한 칸 씩 띄어짐.

```
In [16]: for line in lines :
    ...:     print(line, end='')
    ...: 
Illumination
Light Binding
Prismatic Barrier
Lucent Singularity
Final Spark
In [17]: 
```
- 각 줄에 줄바꿈(\n)문자가 있으므로,
print()함수에 end인자를 주어 줄바꿈을 없앨 수 있다.

### 자동으로 파일 닫기(with)
- 연 파일을 닫지 않을 경우, 파이썬에서는 해당 파일이 
더 이상 사용되지 않을 때 파일을 자동으로 닫아준다.
- with문 내부에서 파일을 사용한 후 구문이 종료되면 자동으로 파일을 닫아주므로,
프로그래밍 단계에서 일일이 파일을 닫아주는 부분에 신경쓰지 않아도 된다.
```python
with 표현식 as 변수
```
```python
In [17]: with open('skills.txt', 'wt') as f:
    ...		f.write(skills)
```


