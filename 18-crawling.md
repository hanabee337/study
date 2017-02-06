http://cryptosan.github.io/pythondocuments/documents/beautifulsoup4/#the-name-argument

### 바로 시작하기에서 따라하기


In [1]: html_doc = """
   ...: <html><head><title>The Dormouse's story</title></head>
   ...: 
   ...: <p class="title"><b>The Dormouse's story</b></p>
   ...: 
   ...: <p class="story">Once upon a time there were three little sisters; and their names were
   ...: <a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
   ...: <a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
   ...: <a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
   ...: and they lived at the bottom of a well.</p>
   ...: 
   ...: <p class="story">...</p>
   ...: """

In [2]: from bs4 import BeautifulSoup

In [3]: soup = BeautifulSoup(html_doc)
/home/hanabee2/.pyenv/versions/3.4.3/envs/fc-python/lib/python3.4/site-packages/bs4/__init__.py:181: UserWarning: No parser was explicitly specified, so I'm using the best available HTML parser for this system ("html.parser"). This usually isn't a problem, but if you run this code on another system, or in a different virtual environment, it may use a different parser and behave differently.

The code that caused this warning is on line 11 of the file /home/hanabee2/.pyenv/versions/fc-python/bin/ipython. To get rid of this warning, change code that looks like this:

 BeautifulSoup([your markup])

to this:

 BeautifulSoup([your markup], "html.parser")

  markup_type=markup_type))

In [4]: soup = BeautifulSoup(html_doc, 'lxml')
---------------------------------------------------------------------------
FeatureNotFound                           Traceback (most recent call last)
<ipython-input-4-9ab035f484df> in <module>()
----> 1 soup = BeautifulSoup(html_doc, 'lxml')

/home/hanabee2/.pyenv/versions/3.4.3/envs/fc-python/lib/python3.4/site-packages/bs4/__init__.py in __init__(self, markup, features, builder, parse_only, from_encoding, exclude_encodings, **kwargs)
    163                     "Couldn't find a tree builder with the features you "
    164                     "requested: %s. Do you need to install a parser library?"
--> 165                     % ",".join(features))
    166             builder = builder_class()
    167             if not (original_features == builder.NAME or

FeatureNotFound: Couldn't find a tree builder with the features you requested: lxml. Do you need to install a parser library?

In [5]: soup.title
Out[5]: <title>The Dormouse's story</title>

In [6]: soup.find('title')
Out[6]: <title>The Dormouse's story</title>

In [7]: soup.title.find('name')

In [8]: soup.title.name
Out[8]: 'title'

In [9]: soup.title.string
Out[9]: "The Dormouse's story"

In [10]: soup.title.parent
Out[10]: <head><title>The Dormouse's story</title></head>

In [11]: type(soup.title.parent)
Out[11]: bs4.element.Tag

In [12]: soup.p
Out[12]: <p class="title"><b>The Dormouse's story</b></p>

In [13]: soup.find('p')
Out[13]: <p class="title"><b>The Dormouse's story</b></p>

In [14]: soup.find_all('a')
Out[14]: 
[<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
 <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
 <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

In [15]: soup.a
Out[15]: <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>

In [16]: soup.find(id='link3')
Out[16]: <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>

In [17]: soup.find_all(class_='sister')
Out[17]: 
[<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
 <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
 <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

In [18]: for link in soup.find_all('a'):
    ...:     print(link.get('href'))
    ...: 
http://example.com/elsie
http://example.com/lacie
http://example.com/tillie

In [19]: print(soup.get_text())

The Dormouse's story
The Dormouse's story
Once upon a time there were three little sisters; and their names were
Elsie,
Lacie and
Tillie;
and they lived at the bottom of a well.
...

- 값이-여럿인 속성
<p class="body strikeout">
class 가 두 개
body, strikeout

- 내려가기


In [20]: soup.name
Out[20]: '[document]'

In [21]: tag.string
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-21-c80e5154c6c4> in <module>()
----> 1 tag.string

NameError: name 'tag' is not defined

In [22]: soup.a
Out[22]: <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>

In [23]: soup.body.b
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-23-8ec437dd9b68> in <module>()
----> 1 soup.body.b

AttributeError: 'NoneType' object has no attribute 'b'

In [24]: soup.head
Out[24]: <head><title>The Dormouse's story</title></head>

In [25]: soup.title
Out[25]: <title>The Dormouse's story</title>

In [26]: soup.body

In [27]: title_tag = soup.title

In [28]: title_tag
Out[28]: <title>The Dormouse's story</title>

In [29]: title_tag.contents
Out[29]: ["The Dormouse's story"]

In [30]: print(type(title_tag.contents))
<class 'list'>

In [31]: head_tag
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-31-cb86da4c96ef> in <module>()
----> 1 head_tag

NameError: name 'head_tag' is not defined

In [32]: head_tag = soup.head

- CSS 선택자 까지 review했음.


- crawling.py에서 이미지 crawling하는 것

