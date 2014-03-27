---
layout: post
title: JavaScript_DOM基础及事件处理
tags: github pages,jekyll,problem
---

{{ page.title }}
================

JavaScript编程与DOM编程
-----------------------

一般来说，JavaScript的web应用程序的组成结构包括：

1. 最底层的JavaScript的核心语言内建对象，这一部分是无法被别的库替代；
2. 客服端DOM+内置宿主对象，这块在下面详解；
3. 服务器端内置宿主对象；
4. 浏览器扩展宿主对象；

首先要理解宿主对象这个概念，有上面可以看出，JavaScript对于不同的运行环境有着不同的内置宿主对象。总的来说导致这个情况的原因是JavaScript是被用来作为一种扩展语言。这里需要理解的是一方面JavaScript作为通用语言，开发者必须拥有运行时的上下文环境；另一方面作为扩展语言需要在内建对象的应用程序（宿主环境）中运行，宿主环境提供上下文信息，JavaScript会以全局对象（window对象）作为根节点的对象树形式接受这些信息，这个对象树就是宿主对象。

DOM编程是浏览器与用户之间的接口，反馈浏览器与用户的交互操作。由于我们大部分对使用JavaScript进行客户端开发，所以我们感觉到这个两种编程是一起的，其实他们拥有相互独立的语言标准。JavaScript为客户端提供对象树的方法有很多，其中DOM就是其中一宿主对象，由此可以看出他就像一个外部库，可以替换，非核心语言。DOM能够很好的将HTML文档以对象树的形式使用所以被JavaScript所引用。

DOM基础
-------

下面为DOM基础操作的讲解和源代码。

源代码：

	...
	<div id="foo">
	<span>a</span>
	<span>b</span>
	<span>c</span>
	<span id='lastspan'>d</span>
	<div id="myid">
		<div id="aa">
			<div id="aaa"></div>
		</div>
		<div id="bb"></div>
	</dvi>
	<div class="xixi haha">
		e
	</div>
	</div>
	<p id="bar">
		<span>x</span>
	</p>

	<script>
		//document是window全局对象的属性，对其属性访问可以省略'window.'
		var foo=document.getElementById("foo");
		alert(foo);//object
		var foospan=foo.getElementsByTagName("span");
		var allspan=document.getElementsByTagName("span");
		alert(foospan.length+allspan.length);//9
		//live 对象
		var newSpan=document.createElement('span');
		newSpan.appendChild(document.createTextNode("f"));
		foo.appendChild(newSpan);
		alert(foospan.length);//5
		//array&&nodelist
		var nodelist=document.getElementsByTagName("span");
		var array=Array.prototype.slice.call(nodelist);//性能更好
		alert(array instanceof Array);//true
		//类名
		var classdiv1=foo.getElementsByClassName("xixi");
		var classdiv2=foo.getElementsByClassName("haha");
		var classdiv3=foo.getElementsByClassName("xixi haha");
		//引用相关元素属性(父、子、兄)
		var my=document.getElementById("myid");
		var elem;
		elem=my.parentNode;
		elem=my.firstElementChild;
		elem=my.lastElementChild;
		var children=my.children;
		alert(children[0].id);
		elem=my.previousElementSibling;
		alert(elem.id);
		elem=my.nextElementSibling;
		elem=elem.nextElementSibling;
		//create modify delete node
		var newSpan=document.createElement('span');
		newSpan.appendChild(document.createTextNode("f"));
		foo.appendChild(newSpan);
		var newcomment=document.createComment("this is a comment!");
		foo.insertBefore(newcomment,my);
		var replaceparent=newcomment.parentNode;
		var replacecomment=document.createComment("this is another comment!");
		replaceparent.replaceChild(replacecomment,newcomment);
		replacecomment.parentNode.removeChild(replacecomment);
		//innerHTML
		var barelem=document.getElementById("bar");
		barelem.innerHTML="<div>xixi</div>"
		barelem.textContent="<div>xixi</div>";//Level 3 core
		//DocumentFragment 提高操作性能,每次操作是内容发生变化，浏览器要重新绘制画面。使用它可以预处理，减少绘画次数。
		var fragment=document.createDocumentFragment();
		var fragmentSpan=document.createElement('span');
		fragmentSpan.appendChild(document.createTextNode("t"));
		fragment.appendChild(fragmentSpan);
		var fragmentSpan1=document.createElement('span');//需要新的对象，同意对象不会再次插入
		fragmentSpan.appendChild(document.createTextNode("t"));
		fragment.appendChild(fragmentSpan1);
		//fragmentSpan.innerHTML("xixi");//这种做法是错误的
		fragment.appendChild(fragmentSpan);
		foo.appendChild(fragment);

	</script>



#### 一些网址：
	
1.	阮一峰的网络日志"搭建一个免费的，无限流量的Blog"：<http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html>
2.	jekyll模版：<https://github.com/jekyll/jekyll/wiki/Sites>
3.	Jekyll插件：<https://github.com/dnfehren/SublimeJekyll>
4.	Git插件：<https://github.com/kemayo/sublime-text-2-git>
5.  Jekyll官网：<http://jekyllcn.com/docs/home/>
6.	很好用的编辑器“Sublime官网”：<http://www.sublimetext.com/>



{% include references.md %}
{% include pictures.md %}
