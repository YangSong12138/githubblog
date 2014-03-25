---
layout: post
title: github使用jekyll免费建站方法和注意事项
tags: github pages,jekyll,problem
---

{{ page.title }}
================

github Pages可以被认为是用户编写的、托管在github上的静态网页.
Jekyll是一个静态站点生成器，它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能，所以实际上可以用来编写整个网站.
我们可以在本地编写符合Jekyll规范的网站源码，生成站点，发布到github上面，这样我们就有了一个免费的，无限流量的，有人维护的属于我们的自己的web网站。
jekyll目录结构
--------------

源代码目录：

	aptitude install libtool // Apache
	aptitude install libxml2-dev
	aptitude install libmcrypt-dev // PHP
	aptitude install libc6-dev gcc g++ make
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


#### 一些网址：

0.	Sublime官网：<http://www.sublimetext.com/>
1.	文档1：<http://www.sublimetext.com/docs/2/>
2.	文档2：<http://docs.sublimetext.info/en/latest/index.html>
3.	Package Control：<http://wbond.net/sublime_packages/package_control/installation>
4.	Jekyll插件：<https://github.com/dnfehren/SublimeJekyll>
5.	Git插件：<https://github.com/kemayo/sublime-text-2-git>



{% include references.md %}
{% include pictures.md %}
