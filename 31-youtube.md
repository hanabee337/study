#### 2017.02.22 - 실습 내용 중에서
- custom user setting 기본 프로세스
- django custom user admin 검색
- django view get parameters
- Youtube Data API v3
	search
		list

#### 170223 | Youtube Bookmark Homework3
##### request.user.bookmarkvideo_set에 대한 검증 테스트
```python
>>> u = MyUser.objects.first()
>>> u
<MyUser: admin>
>>> u.bookmarkvideo_set
<django.db.models.fields.related_descriptors.create_reverse_many_to_one_manager.<locals>.RelatedManager object at 0x7fc92da8e048>
>>> u.bookmarkvideo_set.filter(video__youtube_id='qAuTjBTucz8')
<QuerySet [<BookmarkVideo: BookmarkVideo object>]>
>>> b_list = u.bookmarkvideo_set.filter(video__youtube_id='qAuTjBTucz8')
>>> for b in b_list:
...     print(b)
... 
BookmarkVideo object
>>> 
```