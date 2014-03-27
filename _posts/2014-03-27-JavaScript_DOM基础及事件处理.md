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

	1.最底层的JavaScript的核心语言内建对象，这一部分是无法被别的库替代；
	2.客服端DOM+内置宿主对象，这块在下面详解；
	3.服务器端内置宿主对象；
	4.浏览器扩展宿主对象；

	首先要理解宿主对象这个概念，有上面可以看出，JavaScript对于不同的运行环境有着不同的内置宿主对象。总的来说导致这个

情况的原因是JavaScript是被用来作为一种扩展语言。这里需要理解的是一方面JavaScript作为通用语言，开发者必须拥有运行时的

上下文环境；另一方面作为扩展语言需要在内建对象的应用程序（宿主环境）中运行，宿主环境提供上下文信息，JavaScript会以全

局对象（window对象）作为根节点的对象树形式接受这些信息，这个对象树就是宿主对象。



--------------

源代码目录：

	...
	|-- _config.yml
	|-- _includes
	|-- _layouts
	|   |-- default.html
	|   |-- post.html
	|-- _posts
	|   |-- 20011-10-25-open-source-is-good.html
	|   |-- 20011-04-26-hello-world.html
	|-- _site
	|-- index.html
	|-- assets
	   |-- css
	       |-- style.css
	   |-- javascripts

目录结构详解

<table style="border:#000000 solid;border-width:2 0 0 2">
	<tr>
		<th>文件 / 目录</th>
		<th>描述</th>
	</tr>
	<tr>
		<td style="border:#000000 solid;border-width:1 0 0 1">Other Files/Folders</td>
		<td style="border:#000000 solid;border-width:1 0 0 1">其他一些未被提及的目录和文件如  css 还有 images 文件夹， favicon.ico 等文件都将被完全拷贝到生成的 site 中。</td>
	</tr>
</table>

#### 一些网址：
	
1.	阮一峰的网络日志"搭建一个免费的，无限流量的Blog"：<http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html>
2.	jekyll模版：<https://github.com/jekyll/jekyll/wiki/Sites>
3.	Jekyll插件：<https://github.com/dnfehren/SublimeJekyll>
4.	Git插件：<https://github.com/kemayo/sublime-text-2-git>
5.  Jekyll官网：<http://jekyllcn.com/docs/home/>
6.	很好用的编辑器“Sublime官网”：<http://www.sublimetext.com/>



{% include references.md %}
{% include pictures.md %}
