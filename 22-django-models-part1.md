# Models
- 각각의 모델은 python 클래스
- 모델의 각 속성들은 DB의 field
- 일반적으로 각 모델은 DB 테이블 하나에 mapping된다.

## Quick example
```django
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
```
- ```Person``` is a **```model```** 
- ```first_name, last_name``` are **```fields```** of the model.
- each field is specified as ```a class attribute``` 
- each attribute maps to ```a database column```

## Using models
- Once you have defined your models, 
you need to tell Django you’re going to use those models.
-  Do this by editing your settings file 
and changing the INSTALLED_APPS setting 
to add the name of the module that contains your models.py.
- if the module is created by manage.py startapp script,
the module's name should read in INSTALLED_APPS.
- When you add new apps to INSTALLED_APPS, 
be sure to run ```manage.py migrate```, 
optionally making migrations for them first 
with ```manage.py makemigrations```

## Fields
- The most important part of a model – and the only required part of a model – 
is the list of database fields it defines. 
- Fields are specified by class attributes.

### Field types
- Each field in your model should be an instance of the appropriate Field class.
ex) title = models.**```CharField```**(max_length=200)

### Field options
- Each field takes a certain set of field-specific arguments 
(documented in the [model field reference](https://docs.djangoproject.com/en/1.10/ref/models/fields/#model-field-types)
ex) title = models.CharField(**```max_length```**=200)

### Primary key
- Primary key란 column을 고유하게 구분해 주는 최소의 정보.
- example)

		학생
학번	|이름|	학년|	학과
--|--|--|--
100|	김씨|	4|	정보통신
200|	이씨|	3|	전파공학
300|	박씨|	1|	정보통신
400|	조씨|	4|	전파공학
500|	임씨|	2|	컴퓨터공학

- 학생 테이블에서 학번 속성이나 이름 속성은 테이블 내의 행을
 유일하게 식별할 수 있으므로 기본키로 사용될 수 있다.
 
- The primary key field is read-only. 
- If you change the value of the primary key 
on an existing object and then save it, 
a new object will be created alongside the old one.
```
from django.db import models

class Fruit(models.Model):
    name = models.CharField(max_length=100,
     primary_key=True)
```
```
>>> fruit = Fruit.objects.create(name='Apple')
>>> fruit.name = 'Pear'
>>> fruit.save()
>>> Fruit.objects.values_list('name', flat=True)
['Apple', 'Pear']
```

### Automatic primary key fields
- Each model requires exactly one field to have primary_key=True
(either explicitly declared or automatically added).
- This is an auto-incrementing primary key (Q)?

### Verbose field names
- Except for ForeignKey, ManyToManyField and OneToOneField,
Each field type takes an optional ```first positional argument``` – a ```verbose name```.
- ForeignKey, ManyToManyField and OneToOneField
require the first argument to be a model class, 
so use the verbose_name keyword argument:
- example) in case of ForeignKey, 
```
poll = models.ForeignKey(
    Poll,
    on_delete=models.CASCADE,
    verbose_name="the related poll",
)
```
### Foreign key
- 외래 키(FK)는 두 테이블의 데이터 간 연결을 설정하고
 강제 적용하는 데 사용되는 열입니다. 
- 테이블을 만들거나 수정할 때 FOREIGN KEY 제약 조건을 
 정의하여 외래 키를 만들 수 있습니다.
- 외래 키 참조에서는 한 테이블의 기본 키 값을 가지고 있는 열을
 다른 테이블의 열이 참조할 때 두 테이블 간에 연결이 생성됩니
 다. 이때 두 번째 테이블에 추가되는 열이 외래 키가 됩니다.

- ex)
![foreign key](imgs/foreign-key.gif  "foreign key")

### Relationships
- power of relational databases lies in relating tables to each other
- three most common types of database relationships:
	1. many-to-one, 
	2. many-to-many
	3. one-to-one.

#### Many-to-one relationships
- To define a many-to-one relationship, 
use django.db.models.ForeignKey.

- ForeignKey requires a positional argument: 
the class to which the model is related.

ex) For example, if a Car model has a Manufacturer – 
that is, a Manufacturer makes multiple cars 
but each Car only has one Manufacturer 

>from django.db import models
>
>class **```Manufacturer```**(models.Model):
    # ...
    pass
>
>class **```Car```**(models.Model):
    manufacturer = models.ForeignKey(**```Manufacturer```**, 
    on_delete=models.CASCADE)
    # ...

#### ForeignKey &Recursive Relationship
- You can also create [recursive relationship](https://docs.djangoproject.com/en/1.11/ref/models/fields/#recursive-relationships)  (an object with a many-to-one relationship to itself
 - To create a recursive relationship – an object that has a many-to-one relationship with itself – use ```models.ForeignKey```(**```'self'```**, on_delete=models.CASCADE).
- [Many-to-one relationship model example](https://docs.djangoproject.com/en/1.10/topics/db/examples/many_to_one/)

- 실습
```python
In [1]: from person.models import Person
In [2]: instructor = Person.objects.get(name='이한영')
In [3]: p1 = Person.objects.get(name='최용일')
In [4]: p2 = Person.objects.get(name='김정호')
In [5]: p1.instructor = instructor
In [6]: p2.instructor = instructor
In [7]: p1.save()
In [8]: p2.save()
In [9]: p1.instructor
Out[9]: <Person: 이한영>

In [10]: p2.instructor
Out[10]: <Person: 이한영>

In [11]: instructor
Out[11]: <Person: 이한영>

- 강사가 학생을 역참조하고자 하는 경우 (클래스 소문자 + _set : person_set)
In [12]: instructor.person_set.all()
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-12-0adadd0a316b> in <module>()
----> 1 instructor.person_set.all()

AttributeError: 'Person' object has no attribute 'person_set'

그런데, 여기서 에러가 발생했다. 
이유는 코드에 related_name = 'student_set'으로 지정하였기 때문.
related_name이 지정되어 있지 않았다면, (클래스 소문자 + _set)의 조합인 person_set으로 검색이 가능했을 것이다.
만약, 외래키가 여러 개인 경우, related_name을 지정하지 않으면 모두 person_set이라는 동일 이름을 갖기 때문에, migrations시 충돌이 발생한다.

In [13]: instructor.person-set
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-13-115492178986> in <module>()
----> 1 instructor.person-set

AttributeError: 'Person' object has no attribute 'person'

In [14]: instructor.person_set
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-14-0bdcb0a5d095> in <module>()
----> 1 instructor.person_set

AttributeError: 'Person' object has no attribute 'person_set' : 코드 상에 related_name이 student_set으로 설정되어 있어서 안된 것임.

In [15]: instructor.student_set 
Out[15]: <django.db.models.fields.related_descriptors.create_reverse_many_to_one_manager.<locals>.RelatedManager at 0x7fe30cb8ddd8>

In [16]: instructor.student_set.all()
Out[16]: <QuerySet [<Person: 최용일>, <Person: 김정호>]>
```

#### flat=True
- [flat](https://docs.djangoproject.com/en/1.10/ref/models/querysets/)
-  ```flat = True```로 하면, tutple이지만, 인자가 하나밖에 없는 경우, list로 뽑아올 수 있다.
- If you only pass in a single field, you can also pass in the flat parameter. 
- If True, this will mean the returned results are single values, rather than one-tuples.

#### Many-to-many relationships
- It doesn’t matter which model has the ManyToManyField, 
but you should only put it in one of the models – not both.

- 실습
- shell에서 객체 생성, instance 받아오는 것들 익숙해지기.

- For example, if a Pizza has multiple Topping objects – that is, 
a Topping can be on multiple pizzas and each Pizza has multiple toppings
- ManyToMany 관계에서는 아무나 역참조가 되지만,
포함관계에서 상위요소에 해당하는 클래스에 ManyToMany를 선언한다.

```python
from django.db import models

class Topping(models.Model):
    # ...
    pass

class Pizza(models.Model):
    # ...
    toppings = models.ManyToManyField(Topping)
```

```python
- ManyToMany Relationship

>>> from pizza.models import Pizza, Topping
>>> cp = Pizza.objects.create(title='Cheese Pizza') : create는 save한 결과까지 포함.
>>> bp = Pizza.objects.create(title='Bulgogi Pizza')
>>> pp = Pizza.objects.create(title='Pepproni Pizza')
>>> Pizza.objects.all()
<QuerySet [<Pizza: Cheese Pizza, (Toppings : )>, 
<Pizza: Bulgogi Pizza, (Toppings : )>, <Pizza: Pepproni Pizza, (Toppings : )>]>
>>> Pizza.objects.values_list('title', flat=True)
<QuerySet ['Cheese Pizza', 'Bulgogi Pizza', 'Pepproni Pizza']>
>>> Pizza.objects.values_list('title', flat=True)
<QuerySet ['Cheese Pizza', 'Bulgogi Pizza', 'Pepproni Pizza']>

>>> t_pimang = Topping.objects.create(title = 'Pimang')
>>> t_cheese = Topping.objects.create(title = 'Cheese')
>>> t_mush = Topping.objects.create(title = 'Mushroom')
>>> t_ham = Topping.objects.create(title = 'Ham')
>>> Topping.objects.values_list('title', flat=True)
<QuerySet ['Pimang', 'Cheese', 'Mushroom', 'Ham']>
>>> cp.toppins = (t_cheese, t_ham) <- 한 개 add시, cp.toppings.add(t_ham) 표현도 가능.
>>> bp.toppings = (t_cheese, t_mush, t_pimang) <- 여러 개 add시
>>> pp.toppings = (t_cheese, t_pimang, t_mush, t_ham)
>>> cp
<Pizza: Cheese Pizza, (Toppings : )>
>>> bp
<Pizza: Bulgogi Pizza, (Toppings : Pimang,Cheese,Mushroom)>
>>> pp
<Pizza: Pepproni Pizza, (Toppings : Pimang,Cheese,Mushroom,Ham)>
>>> cp.toppings = (t_cheese, t_ham)
>>> 
>>> 
>>> cp.toppings.all()
<QuerySet [<Topping: Cheese>, <Topping: Ham>]>
>>> cp.toppings.values_list('title')
<QuerySet [('Cheese',), ('Ham',)]>
>>> cp.toppings.values_list('title', flat=True)
<QuerySet ['Cheese', 'Ham']>
>>> ','.join(cp.toppings.values_list('title', flat=True))
'Cheese,Ham'
```

- DB Browser SQLite3로 확인해보면,
	- 피자(P) <-> 토핑(T)사이에 테이블이 있다. 이게 pizza_pizza_toppings 이다. 
DB Browser에서 DB 구조를 확인해 봤을 때.
피자와 토핑사이에 있는 테이블(P-T테이블)에 피자 id를 올려, 피자를 테이블에 올리고, 
각각의 토핑도 P-T 테이블에 올려서, P-T 테이블에 있는 id에 딸린 topping들을 확인하는 것이
ManyToMany 관계형이다.

```python
(InteractiveConsole)
> from person.models import User
> u1= user.objects.create(name='bhj')
> u2= User.objects.create(name='hhh')
> u1.friends.add(u2)
> u1.friends.all()
<QuerySet [<User: hhh>]>
> u2.friends.all()
<QuerySet [<User: bhj>]>
> 
```

- 위의 내용은 u1에서만 u2를 add했는데, 
u2도 자동으로 u1을 friend로 추가가 되어 있다.

```python
symmetrical=False, 이 설정을 해줘야 서로 following되는 걸 막을 수 있다.

> u1=User.objects.create(name='Me')
> u2=User.objects.creat(name='you')
Traceback (most recent call last):
  File "<console>", line 1, in <module>
AttributeError: 'Manager' object has no attribute 'creat'
> u2=User.objects.create(name='you')
> u1.followers.add(u2)
> u1.followers.all()
<QuerySet [<User: you>]>
> u2.followers.all()
<QuerySet []>

- symmetrical=False, 이 설정이 안되어 있을 시 실행 결과,

> from person.models import User,Person
> u1=User.objects.create(name='Me')
> u2=User.objects.create(name='You')
> u1.followers.add(u2)
> u1.followers.all()
<QuerySet [<User: You>]>
> u2.followers.all()
<QuerySet [<User: Me>]>
>
```

- 한 개 필드만 있어도 된다. User 클래스에서
followers, following 두 개 필드가 있는데,
following 필드를 지워도 
symmetrical=False, 이 설정이 되어 있어서
from-to 관계가 있기 때문에 u2.followers.all()의 결과가
위의 것과 다르다. 
```python
 from person.models import User,Person
 u1=User.objects.create(name='Me')
 u2=User.objects.create(name='He')
 u1.followers.add(u2)
 u1.followers.all()
<QuerySet [<User: He>]>
 u2.followers.all()
<QuerySet []>
```

### related_name
- The related_name attribute specifies the name of the reverse 
relation from the User model back to your model.

- If you don't specify a related_name, Django automatically creates 
one using the name of your model with the suffix ```_set```, 
for instance, User.map_set.all().

- If you do specify, e.g. related_name=maps on the User model, 
User.map_set will still work, but the User.maps.

	- [related_name](http://stackoverflow.com/questions/2642613/what-
is-related-name-used-for-in-django)

### symmetrical
- symmetrical=True results in creating two rows for a single 
relationship between two objects because it is bidirectional. 
For example: If A is a friend of B, then B is a friend of A so we need 
two separate rows in the friends table where first one will indicate 
the relation A -> B and second one is B -> A

	- [symmetrical](https://docs.djangoproject.com/en/1.11/ref/models/fields/#django.db.models.ManyToManyField.symmetrical) 
	- [symmetrical2](http://stackoverflow.com/questions/36852324/in-
django-what-does-symmetrical-true-do) 

- If you do ```not want symmetry in many-to-many relationships with self```, 
```set symmetrical to False```. This will force Django to add the descriptor for the reverse relationship,
allowing ManyToManyField relationships to be non-symmetrical.

### through_field vs through
- ```through``` 
	- Django allows you to specify the model that will
	 be used ```to govern``` the many-to-many relationship. 
	- You can then put ```extra fields``` on the intermediate mode
	- The most common use for this option is when 
	you want ```to associate extra data``` with a many-to-many relationship
	- [through](https://docs.djangoproject.com/en/1.11/ref/models/fields/#django.db.models.ManyToManyField.through) 

```python
from django.db import models

class Person(models.Model):
    name = models.CharField(max_length=128)

    def __str__(self):              # __unicode__ on Python 2
        return self.name

class Group(models.Model):
    name = models.CharField(max_length=128)
    members = models.ManyToManyField(Person, through='Membership')

    def __str__(self):              # __unicode__ on Python 2
        return self.name

class Membership(models.Model):
    person = models.ForeignKey(Person, on_delete=models.CASCADE)
    group = models.ForeignKey(Group, on_delete=models.CASCADE)
    date_joined = models.DateField()
    invite_reason = models.CharField(max_length=64)
```

- ```through_field```
	- Only used when a custom intermediary model is specified
	- If Membership has two foreign keys to Person (person and inviter), which makes the relationship ambiguous and Django can’t know which one to use.
	- In this case, you must ```explicitly specify which foreign keys``` Django should use using ```through_fields```
	- [through_fields](https://docs.djangoproject.com/en/1.11/ref/models/fields/#django.db.models.ManyToManyField.through_fields) 

```python
from django.db import models

class Person(models.Model):
    name = models.CharField(max_length=50)

class Group(models.Model):
    name = models.CharField(max_length=128)
    members = models.ManyToManyField(
        Person,
        through='Membership',
        through_fields=('group', 'person'),
    )

class Membership(models.Model):
    group = models.ForeignKey(Group, on_delete=models.CASCADE)
    person = models.ForeignKey(Person, on_delete=models.CASCADE)
    inviter = models.ForeignKey(
        Person,
        on_delete=models.CASCADE,
        related_name="membership_invites",
    )
    invite_reason = models.CharField(max_length=64)
```
	
#### One-to-one relationships
- This is most useful on the primary key of an object
when that object “extends” another object in some way.(?)
- OneToOneField requires a positional argument: 
the class to which the model is related.
- one-to-one vs inheritance (?)
- [One-to-one relationship model example ](https://docs.djangoproject.com/en/1.10/topics/db/examples/one_to_one/) 

### Models across file
- OK to relate a model to one from another app. 
- To do this, import the related model 
at the top of the file where your model is defined.
- Then, just refer to the other model class wherever needed.

### Field name restrictions
- A field name cannot be a Python reserved word,
 because that would result in a Python syntax error. 
- A field name cannot contain more than one underscore in a row 
due to the way Django’s query lookup syntax works.

## Meta options
- Model metadata is “anything that’s not a field”
- Give your model metadata by using an inner **```class Meta```**

## Model attributes
- The most important attribute of a model is the **```Manager```**
-  **```Manager```** is the interface through which database query operations are provided to Django models
-  and is used to retrieve the instances from the database.
- Managers are only accessible via model classes, 
not the model instances(?)

## Model method
- model methods should act on a particular model instance
-  ```\_\_str\_\_()```
- get_absolute_url() : 
	- This tells Django how to calculate the URL for an object.
	- Django uses this any time it needs to figure out a URL for an object.
	
### Overriding perdefined model methods
- You’re free to override any other model method to alter behavior.
- A classic use-case for overriding the built-in methods is 
if you want something to happen whenever you save an object.

For example,
```python
from django.db import models

class Blog(models.Model):
    name = models.CharField(max_length=100)
    tagline = models.TextField()

    def save(self, *args, **kwargs):
        do_something()
        super(Blog, self).save(*args, **kwargs) 
        # Call the "real" save() method.
        do_something_else()
```
```python
from django.db import models

class Blog(models.Model):
    name = models.CharField(max_length=100)
    tagline = models.TextField()

    def save(self, *args, **kwargs):
        if self.name == "Yoko Ono's blog":
            return # Yoko shall never have her own blog!
        else:
            super(Blog, self).save(*args, **kwargs) 
            # Call the "real" save() method.
```
- It’s also important that you pass through the arguments 
that can be passed to the model method

### Executing custom SQL
- Another common pattern is writing custom SQL statements in model methods and module-level methods using raw SQL.
