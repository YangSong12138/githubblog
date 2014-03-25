---
layout: post
title: github使用jekyll免费建站方法和注意事项
tags: github pages,jekyll,problem
---

{{ page.title }}
================

技术简介
--------

github Pages可以被认为是用户编写的、托管在github上的静态网页.

Jekyll是一个静态站点生成器，它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能，所以实际上可以用来编写整个网站.

我们可以在本地编写符合Jekyll规范的网站源码，生成站点，发布到github上面，这样我们就有了一个免费的，无限流量的，有人维护的属于我们的自己的web网站。

优点
----

空间免费，github托管，稳定又安全；

允许本地服务器调试，使用git命令同步来管理文章，版本控制，一键恢复；

允许绑定顶级域名；

文章用markedown编写；

缺点
----
一定的技术门槛，要懂一点git和网页开发。

生成的是静态网页，添加动态功能必须使用外部服务，比如评论功能就只能用disqus。

不适合大型网站，因为没有用到数据库，每运行一次都必须遍历全部的文本文件，网站越大，生成时间越长。

jekyll目录结构
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

<table border="1px">
	<tr>
		<th>文件 / 目录</th>
		<th>描述</th>
	</tr>
	<tr>
		<td>Other Files/Folders</td>
		<td>其他一些未被提及的目录和文件如  css 还有 images 文件夹， favicon.ico 等文件都将被完全拷贝到生成的 site 中。</td>
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
