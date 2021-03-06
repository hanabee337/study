# Built-in template tags and filters

### autoescape
- Controls the current auto-escaping behavior. 
- This tag takes either on or off as an argument and that determines whether auto-escaping is in effect inside the block. 
- The block is closed with an endautoescape ending tag
- When auto-escaping is in effect, all variable content has HTML escaping applied to it 
before placing the result into the output

```html
{% autoescape on %}
    {{ body }}
{% endautoescape %}
```

### comment
- Ignores everything between {% comment %} and {% endcomment %}

```html
<p>Rendered text with {{ pub_date|date:"c" }}</p>
{% comment "Optional note" %}
    <p>Commented out text with {{ create_date|date:"c" }}</p>
{% endcomment %}
```

### csrf_token
- This tag is used for CSRF protection, as described in the documentation for [Cross Site Request Forgeries](https://docs.djangoproject.com/en/1.11/ref/csrf/)
	
### **```cycle```**
- Produces one of its arguments each time this tag is encountered.
- The first argument is produced on the first encounter, the second argument on the second encounter, and so forth
- Once all arguments are exhausted, the tag cycles to the first argument and produces it again.
- The first iteration produces HTML that refers to class row1, the second to row2, the third to row1 again, and so on for each iteration of the loop.

```html
{% for o in some_list %}
    <tr class="{% cycle 'row1' 'row2' %}">
        ...
    </tr>
{% endfor %}
```
- In some cases you might want to refer to the current value of a cycle without advancing to the next value. 
To do this, just give the {% cycle %} tag a name, using “as”, like this:

```html
{% cycle 'row1' 'row2' as rowcolors %}
```

### ```extends```
- Signals that this template extends a parent template. 
```html
{% extends "base.html" %} (with quotes) 
```
- uses the literal value "base.html" as the name of the parent template to extend.

### **```filter```**
```
{% filter force_escape|lower %}
    This text will be HTML-escaped, and will appear in all lowercase.
{% endfilter %}
```

### firstof
- Outputs the first argument variable that is not False.
```html
{% firstof var1 var2 var3 %}
```
is eqivalnet to 

```html
{% if var1 %}
    {{ var1 }}
{% elif var2 %}
    {{ var2 }}
{% elif var3 %}
    {{ var3 }}
{% endif %}
```

### **```for```**
- Loops over each item in an array, making the item available in a context variable

```html
{% for athlete in athlete_list %}
    <li>{{ athlete.name }}</li>
{% endfor %}
```

- You can loop over a list in reverse by using {% for obj in list reversed %}.

- This can also be useful if you need to access the items in a dictionary.

```html
{% for key, value in data.items %}
    {{ key }}: {{ value }}
{% endfor %}
```

|Variable|	Description|
---|---
forloop.counter	| The current iteration of the loop (1-indexed)
forloop.counter0	| The current iteration of the loop (0-indexed)
forloop.revcounter	|The number of iterations from the end of the loop (1-indexed)
forloop.revcounter0	|The number of iterations from the end of the loop (0-indexed)
forloop.first	|True if this is the first time through the loop
forloop.last	|True if this is the last time through the loop
forloop.parentloop	|For nested loops, this is the loop surrounding the current one


### for ... empty
- The for tag can take an optional {% empty %} clause whose text is displayed if the given array is empty or could not be found:

```html
<ul>
{% for athlete in athlete_list %}
    <li>{{ athlete.name }}</li>
{% empty %}
    <li>Sorry, no athletes in this list.</li>
{% endfor %}
</ul>
```

### **```if```**
- Boolean operators

```html
{% if athlete_list and coach_list %}
    Both athletes and coaches are available.
{% endif %}

{% if not athlete_list %}
    There are no athletes.
{% endif %}

{% if athlete_list or coach_list %}
    There are some athletes or some coaches.
{% endif %}

{% if not athlete_list or coach_list %}
    There are no athletes or there are some coaches.
{% endif %}

{% if athlete_list and not coach_list %}
    There are some athletes and absolutely no coaches.
{% endif %}
```

- Use of actual parentheses in the if tag is invalid syntax. If you need them to indicate precedence, you should use nested if tags.
```html
if (athlete_list and coach_list) or cheerleader_list
```

- == operator
- != operator
- < operator
- \> operator
- \<= operator
- \>= operator
- in operator
	```{% if user in users %}
  	If users is a QuerySet, this will appear if user is an
  	instance that belongs to the QuerySet.
	{% endif %}
	```
- not in operator
- is operator
- is not operator

### Filters
- You can also use filters in the if expression.

```html
{% if messages|length >= 100 %}
   You have lots of messages today!
{% endif %}
```

### Complex expressions
- All of the above can be combined to form complex expressions.
	- or
	- and
	- not
	- in
	- ==, !=, <, >, <=, >=
	
```html
{% if a == b or c == d and e %}
```

### ifchanged
- Check if a value has changed from the last iteration of a loop.
- {% ifchanged %} block tag is used within a loop.
```html
{% for match in matches %}
<div style="background-color:
{% ifchanged match.ballot_id %}
	{% cycle "red" "blue" %}
{% else %}
	gray
{% endifchanged %}
{{ match }}</div>
{% endfor %}
```
	
### include
- Loads a template and renders it with the current context. This is a way of “including” other templates within a template.
```html
{% include "foo/bar.html" %}
```
- You can pass additional context to the template using keyword arguments:
```html
{% include "name_snippet.html" with person="Jane" greeting="Hello" %}
```
- If you want to render the context only with the variables provided 
(or even no variables at all), use the only option. 
No other variables are available to the included template:
```html
{% include "name_snippet.html" with greeting="Hi" only %}
```

### load
- Loads a custom template tag set.
- For example, the following template would load all the tags and filters registered in somelibrary and otherlibrary located in package package:
```html
{% load somelibrary package.otherlibrary %}
```
- You can also selectively load individual filters or tags from a library, using the from argument. 
In this example, the template tags/filters named foo 
and bar will be loaded from somelibrary:
```html
{% load foo bar from somelibrary %}
```

### lorem
- Displays random “lorem ipsum” Latin text.
```html
{% lorem [count] [method] [random] %}
```
	
|Argument|	Description|
---|---
count|	A number (or variable) containing the number of paragraphs or words to generate (default is 1).
method|	Either w for words, p for HTML paragraphs or b for plain-text paragraph blocks (default is b).
random|	The word random, which if given, does not use the common paragraph (“Lorem ipsum dolor sit amet...”) when generating text.

### now
- Displays the current date and/or time, using a format according to the given string
```html
It is {% now "jS F Y H:i" %}
```

### **```regroup```**
- Regroups a list of alike objects by a common attribute.
- example
```html
	cities = [
    {'name': 'Mumbai', 'population': '19,000,000', 'country': 'India'},
    {'name': 'Calcutta', 'population': '15,000,000', 'country': 'India'},
    {'name': 'New York', 'population': '20,000,000', 'country': 'USA'},
    {'name': 'Chicago', 'population': '7,000,000', 'country': 'USA'},
    {'name': 'Tokyo', 'population': '33,000,000', 'country': 'Japan'},]	
```

- you’d like to display a hierarchical list that is ordered by country, like this:
	- india
		- Mumbai: 19,000,000
		- Calcutta: 15,000,000
	- USA
		- NewYork: 20,000,000
		- Chicago : 6,000,000
	- Japan
		- tokyo :33,000,000

- You can use the {% regroup %} tag to group the list of cities by country. The following snippet of template code would accomplish this
```html
{% regroup cities by country as country_list %}

<ul>
{% for country in country_list %}
    <li>{{ country.grouper }}
    <ul>
        {% for city in country.list %}
          <li>{{ city.name }}: {{ city.population }}</li>
        {% endfor %}
    </ul>
    </li>
{% endfor %}
</ul>
```
- Let’s walk through this example. {% regroup %} takes three arguments: 
the list you want to regroup, the attribute to group by, and the name of the resulting list. 
Here, we’re regrouping the cities list by the country attribute and calling the result country_list.

- {% regroup %} produces a list (in this case, country_list) of group objects. 
Group objects are instances of namedtuple() with two fields:
	- grouper – the item that was grouped by (e.g., the string “India” or “Japan”).
	- list – a list of all items in this group (e.g., a list of all cities with country=’India’).

- Because {% regroup %} produces namedtuple() objects, you can also write the previous example as:
```html
{% regroup cities by country as country_list %}

<ul>
{% for country, local_cities in country_list %}
    <li>{{ country }}
    <ul>
        {% for city in local_cities %}
          <li>{{ city.name }}: {{ city.population }}</li>
        {% endfor %}
    </ul>
    </li>
{% endfor %}
</ul>
```
- Note that {% regroup %} does not order its input!
- Our example relies on the fact that the cities list was ordered by country in the first place.
- If the cities list did not order its members by country, the regrouping would naively display more than one group for a single country.
```html
cities = [
    {'name': 'Mumbai', 'population': '19,000,000', 'country': 'India'},
    {'name': 'New York', 'population': '20,000,000', 'country': 'USA'},
    {'name': 'Calcutta', 'population': '15,000,000', 'country': 'India'},
    {'name': 'Chicago', 'population': '7,000,000', 'country': 'USA'},
    {'name': 'Tokyo', 'population': '33,000,000', 'country': 'Japan'},
]
```
- With this input for cities, the example {% regroup %} template code above would result in the following output:
	- India
		- Mumbai: 19,000,000
	- USA
		- New York: 20,000,000
	- India
		- Calcutta: 15,000,000
	- USA
		- Chicago: 7,000,000
- The easiest solution to this gotcha is to make sure in your view code that the data is ordered according to how you want to display it.
- Another solution is to sort the data in the template using the dictsort filter, if your data is in a list of dictionaries:
```html
{% regroup cities|dictsort:"country" by country as country_list %}
```

### Grouping on other properties


### **```resetcycle```**
- Resets a previous cycle so that it restarts from its first item at its next encounter. 
- Without arguments, {% resetcycle %} will reset the last {% cycle %} defined in the template.

```html
{% for coach in coach_list %}
    <h1>{{ coach.name }}</h1>
    {% for athlete in coach.athlete_set.all %}
        <p class="{% cycle 'odd' 'even' %}">{{ athlete.name }}</p>
    {% endfor %}
    {% resetcycle %}
{% endfor %}
```

```html
<h1>José Mourinho</h1>
<p class="odd">Thibaut Courtois</p>
<p class="even">John Terry</p>
<p class="odd">Eden Hazard</p>

<h1>Carlo Ancelotti</h1>
<p class="odd">Manuel Neuer</p>
<p class="even">Thomas Müller</p>
```
- Notice how the first block ends with class="odd" and the new one starts with class="odd". 
- Without the {% resetcycle %} tag, the second block would start with class="even".

###  spaceless
- Removes whitespace between HTML tags.
- This includes tab characters and newlines.

```html
{% spaceless %}
    <p>
        <a href="foo/">Foo</a>
    </p>
{% endspaceless %}
```

```html
<p><a href="foo/">Foo</a></p>
```

- Only space between tags is removed – not space between tags and text.

### **```templatetag```**
- to display one of the bits used in template tags, you must use the {% templatetag %} tag.

|Argument|	Outputs|
---|---
openblock|	{%|
closeblock	|%}|
openvariable|	{{|
closevariable|	}}|
openbrace|	{|
closebrace|	}|
opencomment|	{#|
closecomment|	#}|

### url
- Returns an absolute path reference (a URL without the domain name) 
matching a given view and optional parameters.

- hard-code URLs in your templates:
```html
{% url 'some-url-name' v1 v2 %}
```
- Do not mix both positional and keyword syntax in a single call. 
All arguments required by the URLconf should be present.

- For example, suppose you have a view, app_views.client, 
whose URLconf takes a client ID (here, client() is a method inside the views file app_views.py). 
The URLconf line might look like this:

```html
('^client/([0-9]+)/$', app_views.client, name='app-views-client')
```

- If this app’s URLconf is included into the project’s URLconf under a path such as this:

```html
('^clients/', include('project_name.app_name.urls'))
```
- then, in a template, you can create a link to this view like this:

```html
{% url 'app-views-client' client.id %}
```

- The template tag will output the string /clients/client/123/.

- Note that if the URL you’re reversing doesn’t exist, you’ll get an NoReverseMatch exception raised, 
which will cause your site to display an error page.

- If you’d like to retrieve a URL without displaying it, 
you can use a slightly different call:

```html
{% url 'some-url-name' arg arg2 as the_url %}
<a href="{{ the_url }}">I'm linking to {{ the_url }}</a>
```

### verbatim
- Stops the template engine from rendering the contents of this block tag.

### widthratio
- For creating bar charts and such, this tag calculates the ratio of a given value to a maximum value, 
and then applies that ratio to a constant.

### with
- Caches a complex variable under a simpler name. 
- This is useful when accessing an “expensive” method multiple times
(e.g., one that hits the database)

```html
{% with total=business.employees.count %}
    {{ total }} employee{{ total|pluralize }}
{% endwith %}
```

- The populated variable (in the example above, total) is only available 
between the {% with %} and {% endwith %} tags.

## Built-in filter reference
### add
- Adds the argument to the value.
```html
{{ value|add:"2" }}
```
- If value is 4, then the output will be 6.

### addslashes
### capfirst
- Capitalizes the first character of the value
```html
{{ value|capfirst }}
```
- If value is "django", the output will be "Django".

### center
- enters the value in a field of a given width.
```html
{{ value|center:"15" }}
```
- If value is "Django", the output will be "     Django    ".

### cut
- Removes all values of arg from the given string
```html
{{ value|cut:" " }}
```
- If value is "String with spaces", the output will be "Stringwithspaces".

### date
- Formats a date according to the given format.

### default
- If value evaluates to False, uses the given default. Otherwise, uses the value.
```html
{{ value|default:"nothing" }}
```
- If value is "" (the empty string), the output will be nothing.

### dictsort
- Takes a list of dictionaries and returns that list sorted by the key given in the argument.
```html
{{ value|dictsort:"name" }}
```
- dictsort can also order a list of lists

### divisibleby
- Returns True if the value is divisible by the argument.
```html
{{ value|divisibleby:"3" }}
```

### filesizeformat
```html
{{ value|filesizeformat }}
```

### first
- Returns the first item in a list.
```html
{{ value|first }}
```

### last
- Returns the last item in a list.
```html
{{ value|last }}
```

### join
- Joins a list with a string, like Python’s str.join(list)
```html
{{ value|join:" // " }}
```
- If value is the list ['a', 'b', 'c'], the output will be the string "a // b // c".

### length
- Returns the length of the value. This works for both strings and lists.
```html
{{ value|length }}
```
- If value is ['a', 'b', 'c', 'd'] or "abcd", the output will be 4.

### linebreaks
```html
{{ value|linebreaks }}
```
- If value is Joel\nis a slug, the output will be <p>Joel<br />is a slug</p>.

### linebreaksbr
- Converts all newlines in a piece of plain text to HTML line breaks (\<br />)
```html
{{ value|linebreaksbr }}
```
- If value is Joel\nis a slug, the output will be Joel<br />is a slug

### ljust
- Left-aligns the value in a field of a given width.
```html
{{ value|ljust:"10" }}
```

### lower
- Converts a string into all lowercase.
```html
{{ value|lower }}
```

### make_list
- Returns the value turned into a list. For a string, it’s a list of characters. For an integer, 
the argument is cast into an unicode string before creating a list.
```html
{{ value|make_list }}
```

### random
- Returns a random item from the given list.
```html
{{ value|random }}
```
- If value is the list ['a', 'b', 'c', 'd'], the output could be "b".

### rjust
- Right-aligns the value in a field of a given width.
```html
{{ value|rjust:"10" }}
```

### slice
- Returns a slice of the list.
```html
{{ some_list|slice:":2" }}
```
- If some_list is ['a', 'b', 'c'], the output will be ['a', 'b'].

### striptags
- Makes all possible efforts to strip all [X]HTML tags.
```html
{{ value|striptags }}
```
- If value is "<b>Joel</b> <button>is</button> a <span>slug</span>", 
- the output will be "Joel is a slug".

### title
- Converts a string into titlecase by making words start with an uppercase character 
and the remaining characters lowercase.
```html
{ value|title }}
```

### truncatechars
- Truncates a string if it is longer than the specified number of characters. 
- Truncated strings will end with a translatable ellipsis sequence (”...”).
```html
{{ value|truncatechars:9 }}
```

### truncatechars_html
- Similar to truncatechars, except that it is aware of HTML tags.
```html
{{ value|truncatechars_html:9 }}
```

### truncatewords
```html
{{ value|truncatewords:2 }}
```

### truncatewords_html
```html
{{ value|truncatewords_html:2 }}
```

### unordered_list
- Recursively takes a self-nested list and returns 
an HTML unordered list – WITHOUT opening and
closing <ul\> tags.

### upper
- Converts a string into all uppercase.
```html
{{ value|upper }}
```

### urlize
- Converts URLs and email addresses in text into clickable links.
```html
{{ value|urlize }}
```

### wordcount
- Returns the number of words.
```html
{{ value|wordcount }}
```
- If value is "Joel is a slug", the output will be 4.

### wordwrap
- Wraps words at specified line length.
- Argument: number of characters at which to wrap the text
```html
{{ value|wordwrap:5 }}
```
- If value is Joel is a slug, the output would be:
```html
Joel
is a
slug
```
### static
- To link to static files that are saved in ```STATIC_ROOT``` Django ships with a static template tag. If the ```django.contrib.staticfiles app``` is installed, 
the tag will serve files using url() method of the storage specified by STATICFILES_STORAGE. For example:
```html
{% load static %}
<img src="{% static "images/hi.jpg" %}" alt="Hi!" />
```