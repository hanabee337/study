#**Emmet Documentation**
---
##**Syntax**

<span style="color: blue; font-size:18px"> **1. Child: >** <span>
```
nav>ul>li
	<nav>
  		<ul>
  			<li></li>
  		</ul>
	</nav>
```  

<span style="color: blue; font-size:18px"> **2. Sibling: +** <span>
```
div+p+bq
	<div></div>
	<p></p>
	<blockquote></blockquote>
```  

<span style="color: blue; font-size:18px"> **3. Climb-up: ^** <span>
```
div+div>p>span+em^bq
<div></div>
<div>
	<p><span></span><em></em></p>
	<blockquote></blockquote>
</div>
	
div+div>p>span+em^^bq
<div></div>
<div>
	<p><span></span><em></em></p>
</div>
<blockquote></blockquote>
```  

<span style="color: blue; font-size:18px"> **4. Item numbering: $** <span>
```
ul>li.item$*5
<ul>
    <li class="item1"></li>
    <li class="item2"></li>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
</ul>  

h$[title=item$]{Header $}*3
<h1 title="item1">Header 1</h1>
<h2 title="item2">Header 2</h2>
<h3 title="item3">Header 3</h3>

ul>li.item$$$*5
<ul>
    <li class="item001"></li>
    <li class="item002"></li>
    <li class="item003"></li>
    <li class="item004"></li>
    <li class="item005"></li>
</ul>  

ul>li.item$@-*5
<ul>
    <li class="item5"></li>
    <li class="item4"></li>
    <li class="item3"></li>
    <li class="item2"></li>
    <li class="item1"></li>
</ul>  

ul>li.item$@3*5
<ul>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
    <li class="item6"></li>
    <li class="item7"></li>
</ul>
```
<span style="color: blue; font-size:18px"> **5. Grouping: ()** <span>
```
div>(header>ul>li*2>a)+footer>p
<div>
    <header>
        <ul>
            <li><a href=""></a></li>
            <li><a href=""></a></li>
        </ul>
    </header>
    <footer>
        <p></p>
    </footer>
</div>  

(div>dl>(dt+dd)*3)+footer>p
<div>
    <dl>
        <dt></dt>
        <dd></dd>
        <dt></dt>
        <dd></dd>
        <dt></dt>
        <dd></dd>
    </dl>
</div>
<footer>
    <p></p>
</footer>
```  

<span style="color: blue; font-size:18px"> **6. Multiplication:*** <span>
```
ul>li*5
<ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>
```  

<span style="color: blue; font-size:18px"> **7. ID and Class attributes** <span>

1.**#header**
```
	<div id="header"></div>
```
2.**.title**
```
<div class="title"></div>
```
3.**form#search.wide**
```
<form id="search" class="wide"></form>
```
4.**p.class1.class2.class3**
```
<p class="class1 class2 class3"></p>
```  

<span style="color: blue; font-size:18px"> **8. Custom attributes** <span>
```
1. p[title="Hello world"]
	<p title="Hello world"></p>
2. td[rowspan=2 colspan=3 title]
	<td rowspan="2" colspan="3" title=""></td>
3. [a='value1' b="value2"]
	<div a="value1" b="value2"></div>
```  

<span style="color: blue; font-size:18px"> **9. Text: {}**<span>
```
1. a{Click me}
	<a href="">Click me</a>
2. p>{Click }+a{here}+{ to continue}
	<p>Click <a href="">here</a> to continue</p>
```  

<span style="color: blue; font-size:18px"> **10. Implicit tag names**<span>
```
1. .class
	<div class="class"></div>
2. em>.class
	<em><span class="class"></span></em>
3. ul>.class
	<ul>
		<li class="class"></li>
	</ul>
4. table>.row>.col
	<table>
		<tr class="row">
			<td class="col"></td>
		</tr>
	</table>
```