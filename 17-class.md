# Class
## 객체지향 프로그래밍
- 파이썬은 모든 것이 객체.
- 객체를 사용할 때는 변수에 해당하는 객체를 참조시켜서 사용하는 것.

### Class란
- 객체를 만들기 위한 틀
### 속성 vs 메서드
- 객체가 가진 ```변수```를 ```속성```이라 하고,
- 객체가 가진 ```함수```를 ```메서드```라 한다.
 
### 인스턴스 vs 객체
- **인스턴스**란 ```클래스의 정의를 통해 만들어진 객체```를 의미한다.
```
[객체와 인스턴스의 차이]

클래스에 의해서 만들어진 객체를 인스턴스라고도 한다.
그렇다면 객체와 인스턴스의 차이는 무엇일까? 이렇게 생각해 보자.
kim = Programmer() 이렇게 만들어진 kim은 객체이다.
그리고 kim이라는 객체는 Programmer의 인스턴스이다.
즉, 인스턴스라는 말은 특정 객체(kim)가 어떤 클래스(Programmer)의 객체인지를
관계 위주로 설명할 때 사용된다.
즉, "kim은 인스턴스" 보다는 "kim은 객체"라는 표현이 어울리며,
"kim은 Programmer의 객체" 보다는 "kim은 Programmer의 인스턴스"라는
표현이 훨씬 잘 어울린다.
```
참조 : <https://wikidocs.net/28>

- Shop이라는 클래스 정의
```python
class Shop:
    def __init__(self, name):
        self.name = name
```
## self 인자.
- 객체의 메서드를 정의할 때, 첫 번째 인수는 항상 ```self```
- ```어떤 인스턴스에서 호출을 했는지 알게 하기 위한 것```이 self인자의 역할
## \_\_init\_\_ 생성자
- ```__init__```은 클래스를 사용한 객체의 초기화 메서드.
- 객체를 생성할 때, 인자를 어떻게 전달받고,
받은 인자를 이용해 어떤 객체를 생성할 지 정의할 수 있다.

- 위의 클래스를 사용하여 객체를 생성
```python
In [1]: from class_sample import Shop
In [2]: lotteria = Shop('Lotteria')
```
위 코드는 하기 순서로 동작함.

	1. Shop 클래스가 정의되었는지 찾는다.
	2. Shop 클래스형 객체를 메모리에 생성한다.
	3. 생성한 객체의 초기화 메서드 __init__을 호출한다.
	4. name값을 저장하고, 만들어진 객체를 반환한다.
	5. lotteria변수에 반환된 객체를 할당한다.
	
### 클래스 속성
```python
class Shop:
    description = 'Python Shop Class'
    def __init__(self, name):
        self.name = name
```
- 어떤 하나의 클래스로부터 생성된 객체들이 같은 값을 가지게 하고 싶을 경우,
```클래스 속성(class attribute)```를 사용한다.
- 객체들에게서 각각의 인스턴스와는 별개의 공통된 메서드를 사용하게 하고 싶을 경우,
```클래스 메서드(class method)```를 사용한다.

## 메서드
1. 인스턴스 메서드
2. 클래스 메서드

### 인스턴스 메서드
- 인스턴스 메서드는 첫 번째 인수로 ```self```를 가진다.
- 인스턴스를 이용해 메서드를 호출할 때, 호출한 인스턴스가 자동으로 전달되며,
- 전달받은 인스턴스는 상태를 확인, 조작하는데에 사용된다.
> **실습**
>	
>	`Shop`클래스의 초기화 메서드 인자로 `shop_type`과 `address`를 추가하고, 해당 인자들을 사용해 객체의 초기값을 만들어준다
>
> `Shop`클래스의 인스턴스 메서드 `show_info`를 아래와 같은 결과를 출력할 수 있도록 수정해본다

```python
>>> shop.show_info()
상점 (롯데리아)
  유형: 패스트푸드
  주소: 서울시 강남구
```

```python
class Shop :
    description = 'Python Shop Class'
    def __init__(self, name, shop_type, addr) :
        self.name = name
        self.shop_type = shop_type
        self.addr = addr

    def show_info(self):
        print('상점 ({})\n 유형: {}\n 주소: {}'.format(self.name, self.shop_type, self.addr))

lotteria = Shop('Lotteria', '패스트푸드', '강남구')
lotteria.show_info()

- 결과
 >> python class_practice.py
상점 (Lotteria)
	유형: 패스트푸드
 	주소: 강남구
```

> **실습**
>	
> `Shop`클래스에 `change_type`인스턴스 메서드를 추가하고, 
상점유형(shop_type)을 변경할 수 있는 기능을 추가한다
> 
> 새로운 `Shop`인스턴스를 하나 생성하고, `show_info()` 인스턴스 메서드를 
> 사용해 본 후 `change_type`메서드를 사용해 `shop_type`을 변경시키고,
> 다시 `show_info()`메서드를 실행해 결과가 잘 반영되었는지 확인한다

```python
class Shop :
    description = 'Python Shop Class'
    def __init__(self, name, shop_type, addr) :
        self.name = name
        self.shop_type = shop_type
        self.addr = addr

    def show_info(self):
        print('상점 ({})\n 유형: {}\n 주소: {}'.format(self.name, self.shop_type, self.addr))

    def change_type(self, new_type):
        self.shop_type = new_type

lotteria = Shop('Lotteria', '패스트푸드', '강남구')
lotteria.show_info()

mac_donald = Shop('Mac-Donald', 'fast-food', '압구정')
mac_donald.show_info()
mac_donald.change_type('junk-food')
mac_donald.show_info()

상점 (Lotteria)
 유형: 패스트푸드
 주소: 강남구
 
상점 (Mac-Donald)
 유형: fast-food
 주소: 압구정
 
상점 (Mac-Donald)
 유형: junk-food
 주소: 압구정
```

### 클래스 메서드
- ```클래스 메서드```는 ```클래스 속성에 대해 동작```하는 메서드이다.
- 위의 인스턴스 메서드와 달리 호출 주체가 클래스이며,
 첫 번째 인자도 클래스이다.
- 첫 번째 인자의 이름은 관용적으로 ```cls```를 사용한다.
- 만약 인스턴스가 첫 번째 인자로 주어지더라도 해당 인자의 클래스로 
자동으로 바뀌어 전달된다.
- ```@classmethod``` 데코레이터를 붙여 사용한다.
- class의 속성보다 instance 의 속성이 우선이다.

> **실습**
>	
> ```Shop```클래스에 클래스 속성 ```description```을 수정하는 클래스 메서드를 작성한다.

```python
class Shop :
    description = 'Python Shop Class'
    def __init__(self, name, shop_type, addr) :
        self.name = name
        self.shop_type = shop_type
        self.addr = addr

    def show_info(self):
        print('상점 ({})\n 유형: {}\n 주소: {}'.format(self.name, 
        self.shop_type, self.addr))

    def change_type(self, new_type):
        self.shop_type = new_type

    @classmethod
    def change_description(cls, new_description):
        cls.description = new_description

    @classmethod
    def show_description(cls):
        print('Class Description : {}'.format(cls.description))

Shop.show_description()
Shop.change_description('이것은 Shop 클래스의 객체이다')
Shop.show_description()

- 결과
Class Description : Python Shop Class
Class Description : 이것은 Shop 클래스의 객체이다
```

## 속성 접근 지정자
###캡슐화 
- 정보를 은닉하는 것
- 객체를 구현할 때, ```사용자가 반드시 알아야 할 데이터나 메서드를 제외한 부분을 
은닉```시켜 ```정해진 방법을 통해서만 객체를 조작```할 수 있도록 하는 방식.
- 그 정도를 속성 접근 지정자로 설정할 수 있다.
- ```property```를 사용해서 접근을 허용한다.
- ```@property``` decorator를 달아주면 사용자는 **```메소드```**를 **```속성```**처럼 사용하게끔 만들어준다.
- 따라서, 메소드의 type을 확인해보면 return해주는 값의 type으로 나온다. 
- 속성 이름을 ```__```로 시작하면, 외부에서의 접근을 제한한다. 
이 경우를 ```private 지정자```라고 한다.
- 실제 이름은 ```_<클래스명>__<속성명>```으로 되어있다
- 파이썬은 속성을 실제로 사용하지 못하도록 숨기지 않고, 
네임 맹글링(name mangling)이라는 기법을 사용한다.

>**실습**
>	
> ```change_type```메서드나 ```change_description```클래스 메서드를 
사용하지 않고도 내부 내용을 변경할 수 있다.
>	
> ```shop_type```의 이름을 ```__shop_type```으로 바꾸고 ```외부에서 직접 변경해본다.```

```python
class Shop :
    description = 'Python Shop Class'
    def __init__(self, name, shop_type, addr) :
        self.name = name
        self.__shop_type = shop_type
        self.addr = addr

    def show_info(self):
        print('상점 ({})\n 유형: {}\n 주소: {}'.format(self.name, self.__shop_type, self.addr))

    def show_type(self):
        print('유형 : {}'.format(self.__shop_type))

print('\n')
mac_donald = Shop('MacDonald', 'fast-food', '압구정')
mac_donald.show_info()
print('\n')
mac_donald.__shop_type = 'junk-food'
mac_donald.show_info()
print('\n')

- 결과
상점 (MacDonald)
 유형: fast-food
 주소: 압구정

상점 (MacDonald)
 유형: fast-food
 주소: 압구정
```

- ```private 지정자```로 속성 이름을 변경하였기 때문에,
```__shop_type```은 외부에서의 직접 변경은 되지 않았다. 
- Q) 그렇담, 어떻게 변경을 하면 되나? 그 정해진 방법이 다음에 나와있다.

## get/set 속성값과 property
- 파이썬에서는 지원하지 않지만, 어떤 언어들은 외부에서 접근할 수 없는 ```private``` 객체 속성을 지원한다.
- 이 경우, 객체에서는 해당 속성을 읽고 쓰기 위해
```getter```, ```setter``` 메서드를 사용해야 한다.

```python
@property
def name(self):
    return self.__name

@name.setter
def name(self, new_name):
    self.__name = new_name
    print('Set new name ({})'.format(self.__name))
```
- ```setter``` property를 명시하지 않으면 읽기전용이 되어 외부에서 조작할 수 없게 된다.

```python

class Shop :
    description = 'Python Shop Class'
    def __init__(self, name, shop_type, addr) :
        self.name = name
        self.__shop_type = shop_type
        self.addr = addr

    def show_info(self):
        print('상점 ({})\n 유형: {}\n 주소: {}'.format(self.name, self.__shop_type, self.addr))

    # private 속성으로 지정이 되었으므로, 변경이 안되어야 하지 않나?
    # Q) property, setter 메서드를 사용하지 않았음에도 왜 변경이 되지? 
    def change_type(self, new_type):
        self.__shop_type = new_type

    def show_type(self):
        print('유형 : {}'.format(self.__shop_type))

    # property, setter 메서드 사용하여 private 속성 값 변경
    # property에 의해 정상 동작함
    # 메서드를 마치 속성 이름처럼 접근을 한다.
    @property
    def shop_type(self):
        return self.__shop_type
    @shop_type.setter
    def shop_type(self, new_type):
        self.__shop_type = new_type
        print('Set new shop type: ({})'.format(self.__shop_type))

    @classmethod
    def change_description(cls, new_description):
        cls.description = new_description

    @classmethod
    def show_description(cls):
        print('Class Description : {}'.format(cls.description))

lotteria = Shop('Lotteria', '패스트푸드', '강남구')
lotteria.show_info()

print('\n')
mac_donald = Shop('MacDonald', 'fast-food', '압구정')
mac_donald.show_info()
print('\n')
# private 속성으로 지정이 되었으므로, 
# Q) __shop_type에 직접 변경하는 것이 안되어야 하지 않나?
# A)밑의 줄에 있는 변수 '__shop_type'와 
# 클래스에서 private 속성으로 정의한 '__shop_type'은
# 서로 다른 변수이다.
# Why? Name Mangling 때문이다
# 따라서, mac_donald.__shop_type = 'junk-food' 여기서 설정한 값이
# 클래스에서 private 속성으로 정의한 '__shop_type'의 값에
# 반영이 되지 않은 것이다.
mac_donald.__shop_type = 'junk-food'
mac_donald.show_info()
print('\n')

# private 속성으로 지정이 되었으므로, 변경이 안되어야 하지 않나?
# Q) property, setter 메서드를 사용하지 않았음에도 왜 변경이 되지? 
mac_donald.change_type('junk-food')
mac_donald.show_info()
print('\n')

# property에 의해 정상 동작함
# 메서드를 마치 속성 이름처럼 접근을 한다.
mac_donald.shop_type = '맛집'
mac_donald.show_info()

print('\n')
Shop.show_description()
Shop.change_description('이것은 Shop 클래스의 객체이다')
Shop.show_description()
```
- 위의 결과에서 보듯,
- **```property, setter decorator```**를 사용하면  
**```해당 메서드```**를 마치 **```속성 이름```**처럼 접근을 할 수가 있다.

## 상속
- 거의 비슷한 기능을 수행하나, 약간의 추가적인 기능이 필요한 다른 클래스가 필요할 경우,
기존의 클래스를 상속받은 새 클래스를 사용하는 형태로 문제를 해결할 수 있다.
- 이 때, 상속 되는 클래스를 부모(상위)클래스라고 하며, 상속을 받는 클래스는 자식(하위)클래스라고 한다.
- 상속받은 ```자식클래스```는 ```부모 클래스```의 **모든 속성과 메서드**를 사용할 수 있다.
- Restaurant 클래스는 Shop 클래스의 속성을 상속받았다.
```python
class Restaurant(Shop):
    pass
```
### 메서드 오버라이드
- 상속받은 클래스에서, ```부모 클래스의 메서드와는 다른 동작```을 하도록 할 수 있는데,
이 경우 **부모 클래스의 메서드를 덮어씌워서 사용**하도록 하며,
이 방법을 ```메서드 오버라이드(method override)```라고 한다.
> **실습**

### 부모 클래스의 메서드를 호출 (super)
- 자식클래스의 메서드에서 부모 클래스에서 사용하는 메서드의 전체를 새로 쓰는것이 아니라,
부모 클래스의 메서드를 호출 후 해당 내용으로 새로운 작업을 해야 할 경우,
```super()메서드```를 사용해서 부모 클래스의 메서드를 직접 호출할 수 있다.
```python
class Restaurant(Shop):
    def __init__(self, name, shop_type, address, rating):
        super().__init__(name, shop_type, address)
        self.rating = rating
```
- 위 코드의 경우, ```super()메서드를 사용```해서 부모의 ```__init__```메서드를 호출한다.

## 다형성
- 같은 함수, 클래스만을 사용하는 것이 아니라,
서로 다른 형태의 객체 메소드인데도 사용가능(?)
- eat이라는 객체를 호출했지만, 실제 이 eat 이라는 메소드가 서로 다른 클래스에 있다. 기능을 다르게 한다.
- 같은 이름의 함수에서 서로 다른 기능을 하는 함수 호출
- 같은 호출에 대해 다른 결과를 갖게 함.
- 다형성을 지원하는 프로그래밍 언어에서는 같은 이름의 함수에서
서로 다른 기능을 하는 방식으로 프로그래밍을 할 수 있다.
- 파이썬에서는 각 객체의 타입과 전혀 상관없이 해당 객체에서 만든
같은 이름의 메서드들을 실행할 수 있다.
```python
# 다형성 예제
class User :
    def __init__(self, name) :
        self.name = name

    def eat_something(self, item) :
        item.eat()

class Food :
    def __init__(self, name) :
        self.name = name

    def eat(self):
        print('{}를 다 먹었다.배 부르다'.format(self.name))

class Drink :
    def __init__(self, name) :
        self.name = name

    def eat(self):
        print('{}를 다 마셨다.갈증 해소'.format(self.name))

user = User('누구')
food1 = Food('햄버거')
drink1 = Drink('게토레이')

user.eat_something(food1)
user.eat_something(drink1)
```
실습
Shop클래스에 클래스 속성 description을 수정하는 클래스 메서드를 작성한다.