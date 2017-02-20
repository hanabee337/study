# MTM
- 실습

```python 
 from person.models import Idol,Group
 from person.models import Idol,Group, Membership
 
 yui = Idol.objects.create(name='유이')
 nana = Idol.objects.create(name='나나')
 gaeun = Idol.objects.create(name='가은')
 lizzy = Idol.objects.create(name='리지')
 laina = Idol.objects.create(name='레이나')
 iyoung=Idol.objects.create(name='이영')
 Idol.objects.values_list('name',flat=True)
<QuerySet ['나나', '레이나', '유이', '나나', '가은', '리지', '레이나', '이영']>
 
 afterschool = Group.objects.create(name='애프터스쿨')
 orangecaramel = Group.objects.create(name='오렌지카라멜')
 m1 = Membership(idol = laina, date_joined=date(2010,6,17)
... 
KeyboardInterrupt
 m1 = Membership(idol = laina, date_joined=date(2010,6,17),group =orangecaramel)
Traceback (most recent call last):
  File "<console>", line 1, in <module>
NameError: name 'date' is not defined
 from datetime import datatime,date,time
Traceback (most recent call last):
  File "<console>", line 1, in <module>
ImportError: cannot import name 'datatime'
 from datetime import datetime,date,time
 m1 = Membership(idol = laina, date_joined=date(2010,6,17),group =orangecaramel)
 m1.save()
/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/fields/__init__.py:1372: RuntimeWarning: DateTimeField Membership.date_joined received a naive datetime (2010-06-17 00:00:00) while time zone support is active.
  RuntimeWarning)
 
 MemberShip.objects.all()
Traceback (most recent call last):
  File "<console>", line 1, in <module>
NameError: name 'MemberShip' is not defined
 Membership.objects.all()
<QuerySet [<Membership: Membership object>]>
 Membership.objects.count()
1
 Membership.objects.create(idol=lizzy, group=orangecaramel, date_joined=date(2010.6,17)
... )
Traceback (most recent call last):
  File "<console>", line 1, in <module>
TypeError: integer argument expected, got float
 
 Membership.objects.create(idol=lizzy, group=orangecaramel, date_joined=date(2010.6,17))
Traceback (most recent call last):
  File "<console>", line 1, in <module>
TypeError: integer argument expected, got float
 Membership.objects.create(idol=lizzy, group=orangecaramel, date_joined=date(2010,6,17))
<Membership: Membership object>
 Membership.objects.count()
2
 Mem
Membership(   MemoryError(  
 Membership.objects.values_list('name',flat=True)
Traceback (most recent call last):
  File "<console>", line 1, in <module>
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 731, in values_list
    clone = self._values(*fields)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 714, in _values
    query.add_fields(field_names, True)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/sql/query.py", line 1644, in add_fields
    "Choices are: %s" % (name, ", ".join(names)))
django.core.exceptions.FieldError: Cannot resolve keyword 'name' into field. Choices are: date_joined, group, group_id, id, idol, idol_id, recommender, recommender_id
 Membership.objects.values_list()
<QuerySet [(1, 7, 2, datetime.datetime(2010, 6, 16, 15, 0, tzinfo=<UTC>), None), (2, 6, 2, datetime.datetime(2010, 6, 16, 15, 0, tzinfo=<UTC>), None)]>
 Membership.objects.values_list('name')
Traceback (most recent call last):
  File "<console>", line 1, in <module>
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 731, in values_list
    clone = self._values(*fields)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 714, in _values
    query.add_fields(field_names, True)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/sql/query.py", line 1644, in add_fields
    "Choices are: %s" % (name, ", ".join(names)))
django.core.exceptions.FieldError: Cannot resolve keyword 'name' into field. Choices are: date_joined, group, group_id, id, idol, idol_id, recommender, recommender_id
 Membership.objects.values_list('id', 'idol__name')
<QuerySet [(2, '리지'), (1, '레이나')]>
 orangecaramel.member.all()
<QuerySet [<Idol: 레이나>, <Idol: 리지>]>
 nana.membership_set.all()
<QuerySet []>
 nana.group_set.all()
<QuerySet []>
 lizzy.group_set.all()
<QuerySet [<Group: 오렌지카라멜>]>
 laina.group_set.all()
<QuerySet [<Group: 오렌지카라멜>]>
 laina.membership_set.values_list('group__name', 'date_joined')
<QuerySet [('오렌지카라멜', datetime.datetime(2010, 6, 16, 15, 0, tzinfo=<UTC>))]>
 
 
 for idol in Idol.objects.all():
     
... for idol in Idol.objects.all():
  File "<console>", line 2
    for idol in Idol.objects.all():
      ^
IndentationError: expected an indented block
 for idol in Idol.objects.all():
...     Mem
Membership(   MemoryError(  
...     Mem
Membership(   MemoryError(  
...     Membership.objects.create(idol=idol, group=afterschool, date_joined=date(2009,1,15))
... 
/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/fields/__init__.py:1372: RuntimeWarning: DateTimeField Membership.date_joined received a naive datetime (2009-01-15 00:00:00) while time zone support is active.
  RuntimeWarning)
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
 afterschool.members.values_list('name')
Traceback (most recent call last):
  File "<console>", line 1, in <module>
AttributeError: 'Group' object has no attribute 'members'
 afterschool.member.values_list('name')
<QuerySet [('나나',), ('레이나',), ('유이',), ('나나',), ('가은',), ('리지',), ('레이나',), ('이영',)]>
 afterschool.member.values_list('id', 'name')
<QuerySet [(1, '나나'), (2, '레이나'), (3, '유이'), (4, '나나'), (5, '가은'), (6, '리지'), (7, '레이나'), (8, '이영')]>
 
 Idol.objects.a
Idol.objects.aggregate(    Idol.objects.annotate(     
Idol.objects.all(          Idol.objects.auto_created  
 Idol.objects.a
Idol.objects.aggregate(    Idol.objects.annotate(     
Idol.objects.all(          Idol.objects.auto_created  
 afterschool.member.all()
<QuerySet [<Idol: 나나>, <Idol: 레이나>, <Idol: 유이>, <Idol: 나나>, <Idol: 가은>, <Idol: 리지>, <Idol: 레이나>, <Idol: 이영>]>
 orangecaramel.member.all()
QuerySet [<Idol: 레이나>, <Idol: 리지>]>
 afterschool.member.de
afterschool.member.deconstruct(  afterschool.member.defer(        
 afterschool.member.de
afterschool.member.deconstruct(  afterschool.member.defer(        
 afterschool.member.del(id=4)
  File "<console>", line 1
    afterschool.member.del(id=4)
                         ^
SyntaxError: invalid syntax
 Idol.objects.filter(membership=None)
<QuerySet []>
 afterschool.member.get(id=4).delete()
(2, {'person.Membership': 1, 'person.Idol': 1})
 afterschool.member.all()
<QuerySet [<Idol: 나나>, <Idol: 레이나>, <Idol: 유이>, <Idol: 가은>, <Idol: 리지>, <Idol: 레이나>, <Idol: 이영>]>
>>> afterschool.member.get(id=6).delete()
(3, {'person.Membership': 2, 'person.Idol': 1})
 afterschool.member.all()
<QuerySet [<Idol: 나나>, <Idol: 레이나>, <Idol: 유이>, <Idol: 가은>, <Idol: 레이나>, <Idol: 이영>]>
 Membership.objects.create(idol=lizzy, group=orangecaramel, date_joined=date(2010.6,17))
Traceback (most recent call last):
  File "<console>", line 1, in <module>
TypeError: integer argument expected, got float
 Membership.objects.create(idol=lizzy, group=orangecaramel, date_joined=date(2010,6,17))
<Membership: Membership object>
 afterschool.member.all()
<QuerySet [<Idol: 나나>, <Idol: 레이나>, <Idol: 유이>, <Idol: 가은>, <Idol: 레이나>, <Idol: 이영>]>
 laina.membership_set.values_list('group__name', 'date_joined')
<QuerySet [('오렌지카라멜', datetime.datetime(2010, 6, 16, 15, 0, tzinfo=<UTC>)), ('애프터스쿨', datetime.datetime(2009, 1, 14, 15=<UTC>))]>
 
 lizzy = Idol.objects.create(name='리지')
 for idol in Idol.objects.all():
...     Membership.objects.create(idol=idol, group=afterschool, date_joined=date(2009,1,15))
... 
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
 
 
 orangecaramel.member.all()
<QuerySet [<Idol: 레이나>]>
 afterschool.member.all()
<QuerySet [<Idol: 나나>, <Idol: 레이나>, <Idol: 유이>, <Idol: 가은>, <Idol: 레이나>, <Idol: 이영>, <Idol: 나나>, <Idol: 레이나>, <은>, <Idol: 레이나>, <Idol: 이영>, <Idol: 리지>]>
 for idol in Idol.objects.all():
...     Membership.objects.create(idol=idol, group=orangecaramel, date_joined=date(2010,1,17))
... 
/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/fields/__init__.py:1372: RuntimeWarning: DateTimeField Membership.date_joined received a naive datetime (2010-01-17 00:00:00) while time zone support is active.
  RuntimeWarning)
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
<Membership: Membership object>
 orangecaramel.member.all()
<QuerySet [<Idol: 레이나>, <Idol: 나나>, <Idol: 레이나>, <Idol: 유이>, <Idol: 가은>, <Idol: 레이나>, <Idol: 이영>, <Idol: 리지>]>
 afterschool.member.all()
<QuerySet [<Idol: 나나>, <Idol: 레이나>, <Idol: 유이>, <Idol: 가은>, <Idol: 레이나>, <Idol: 이영>, <Idol: 나나>, <Idol: 레이나>, <은>, <Idol: 레이나>, <Idol: 이영>, <Idol: 리지>]>
 afterschool.member.get(id=3).delete()
Traceback (most recent call last):
  File "<console>", line 1, in <module>
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 389, in get
    (self.model._meta.object_name, num)
person.models.MultipleObjectsReturned: get() returned more than one Idol -- it returned 2!
 afterschool.member.get(id=6).delete()
Traceback (most recent call last):
  File "<console>", line 1, in <module>
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 385, in get
    self.model._meta.object_name
person.models.DoesNotExist: Idol matching query does not exist.
 orangecaramel.member.get(id=6).delete()
Traceback (most recent call last):
  File "<console>", line 1, in <module>
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 385, in get
    self.model._meta.object_name
person.models.DoesNotExist: Idol matching query does not exist.
 afterschool.member.all()
<QuerySet [<Idol: 나나>, <Idol: 레이나>, <Idol: 유이>, <Idol: 가은>, <Idol: 레이나>, <Idol: 이영>, <Idol: 나나>, <Idol: 레이나>, <은>, <Idol: 레이나>, <Idol: 이영>, <Idol: 리지>]>
 orangecaramel.member.all()
<QuerySet [<Idol: 레이나>, <Idol: 나나>, <Idol: 레이나>, <Idol: 유이>, <Idol: 가은>, <Idol: 레이나>, <Idol: 이영>, <Idol: 리지>]>
 orangecaramel.member.get(id=4).delete()
Traceback (most recent call last):
  File "<console>", line 1, in <module>
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 385, in get
    self.model._meta.object_name
person.models.DoesNotExist: Idol matching query does not exist.
 orangecaramel.member.all()
<QuerySet [<Idol: 레이나>, <Idol: 나나>, <Idol: 레이나>, <Idol: 유이>, <Idol: 가은>, <Idol: 레이나>, <Idol: 이영>, <Idol: 리지>]>
 orangecaramel.member.values_list('id', 'name')
<QuerySet [(7, '레이나'), (1, '나나'), (2, '레이나'), (3, '유이'), (5, '가은'), (7, '레이나'), (8, '이영'), (9, '리지')]>
 orangecaramel.member.get(id=7).delete()
Traceback (most recent call last):
  File "<console>", line 1, in <module>
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 389, in get
    (self.model._meta.object_name, num)
person.models.MultipleObjectsReturned: get() returned more than one Idol -- it returned 2!
 orangecaramel.member.values_list('id', 'name')
<QuerySet [(7, '레이나'), (1, '나나'), (2, '레이나'), (3, '유이'), (5, '가은'), (7, '레이나'), (8, '이영'), (9, '리지')]>
 orangecaramel.member.get(id=2).delete()
(4, {'person.Membership': 3, 'person.Idol': 1})
 orangecaramel.member.values_list('id', 'name')
<QuerySet [(7, '레이나'), (1, '나나'), (3, '유이'), (5, '가은'), (7, '레이나'), (8, '이영'), (9, '리지')]>
 orangecaramel.member.get(id=7).delete()
Traceback (most recent call last):
  File "<console>", line 1, in <module>
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 389, in get
    (self.model._meta.object_name, num)
person.models.MultipleObjectsReturned: get() returned more than one Idol -- it returned 2!
 orangecaramel.member.values_list('id', 'name')
<QuerySet [(7, '레이나'), (1, '나나'), (3, '유이'), (5, '가은'), (7, '레이나'), (8, '이영'), (9, '리지')]>
 orangecaramel.member.get(id='레이나').delete()
Traceback (most recent call last):
  File "<console>", line 1, in <module>
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 376, in get
    clone = self.filter(*args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 796, in filter
    return self._filter_or_exclude(False, *args, **kwargs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/query.py", line 814, in _filter_or_exclude
    clone.query.add_q(Q(*args, **kwargs))
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/sql/query.py", line 1227, in add_q
    clause, _ = self._add_q(q_object, self.used_aliases)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/sql/query.py", line 1253, in _add_q
    allow_joins=allow_joins, split_subq=split_subq,
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/sql/query.py", line 1187, in build_filter
    condition = self.build_lookup(lookups, col, value)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/sql/query.py", line 1083, in build_lookup
    return final_lookup(lhs, rhs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/lookups.py", line 19, in __init__
    self.rhs = self.get_prep_lookup()
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/lookups.py", line 59, in get_prep_lookup
    return self.lhs.output_field.get_prep_value(self.rhs)
  File "/home/hanabee2/.pyenv/versions/3.4.3/envs/djang_docu_env/lib/python3.4/site-packages/django/db/models/fields/__init__.py", line 946, in get_prep_value
    return int(value)
ValueError: invalid literal for int() with base 10: '레이나'
 orangecaramel.member.values_list('id', 'name')
<QuerySet [(7, '레이나'), (1, '나나'), (3, '유이'), (5, '가은'), (7, '레이나'), (8, '이영'), (9, '리지')]>
```

- 중간자 모델을 통해 access도 가능하다.

- OneToOne 관계
예) 개인 추가 프로필 한사람한테만 해당될 경우,

- meta option
해당 클래스에 대한 속성

- 모델 속성
objects
예) model.```objects```.all()

- 모델 메서드
각 row = model의 인스턴스의 필드
property는 함수를 변수처럼 사용할 때. getter/setter 안쓸려구.

- 모델 메서드 overriding
모델 메서드 override가 가능하다.

- Abstract base Classes
몇 가지 공통된 정보를 여러 다른 모델에 넣으려 할때.
abstract = true하면 상속만 받을 뿐, 코드가 존재하진 않음.

python에서 abc는 abstract base classes

- Multi-table inheritance
테이블간 이동이 많아 DB 시스템적으론 비효율적
상위 id만 상속
잘 사용하지 않음.
 
-pecifying the parent link field 
잘 사용하지 않음

- Proxy models
는 부모만 만듬.
같은 객체에 대해 다른 동작을 하게 하고 싶을때
메서드를 서로 다르게 줄 수 있다.
부모 모델 1개에 대해서만 만들 수 있다.

- Multiple inheritance

- 연결된
b = Blog()
p = Post()
p_yesterday, p_tomorrow

Blog를 참조하는 Post중에서 - post_yesterday, post_tomorrow- filtering
1. Blog.objects.filter(post__title__contains='Yesterday', 
post__published_date__day==11)
<QuerySet [무]>
- 못찾음.
1의 경우는 두가지 조건을 모두 만족하는 query를 찾는 것.

2. Blog.objects.filter(post__title__contains='Yesterday').filter(
post__published_date__day==11)
- <QuerySet [유]>
2의 경우는 post 객체 중에서 title이 Yesterday인 객체들 중에서
 published_date가 day=11인 객체를 찾는 것. 

따라서, 1,2의 결과가 다름

### 오늘(2017.02.10) 진도 내용 
 - Meta Options
 - Model Attributes
 - Model methods
 	- override
 - Model Inheritance
 	- Abstract base classes
 		- meta inheritance
 	- Proxy
 		- meta inheritance
 
