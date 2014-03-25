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
------------
<table>
	<tr>
		<th>"文件 / 目录"”"</th>
		<th>"保存配置数据。很多配置选项都会直接从命令行中进行设置，但是如果你把那些配置写在这儿，你就不用非要去记住那些命令了。"</th>
	</tr>
	<tr>
		<td>"_config.yml"</td>
		<td>"保存配置数据。很多配置选项都会直接从命令行中进行设置，但是如果你把那些配置写在这儿，你就不用非要去记住那些命令了。"</td>
	</tr>
	<tr>
		<td>"_drafts"</td>
		<td>"drafts 是未发布的文章。这些文件的格式中都没有 title.MARKUP 数据。"</td>
	</tr>
	<tr>
		<td>"_includes"</td>
		<td>"你可以加载这些包含部分到你的布局或者文章中以方便重用。可以用这个标签  {% include file.ext %} 来把文件 _includes/file.ext 包含进来。"</td>
	</tr>
	<tr>
		<td>"_layouts"</td>
		<td>"layouts 是包裹在文章外部的模板。布局可以在 YAML 头信息中根据不同文章进行选择。 这将在下一个部分进行介绍。标签  {{ content }} 可以将content插入页面中。"</td>
	</tr>
	<tr>
		<td>"_posts"</td>
		<td>"这里放的就是你的文章了。文件格式很重要，必须要符合: YEAR-MONTH-DAY-title.MARKUP。 The permalinks 可以在文章中自己定制，但是数据和标记语言都是根据文件名来确定的。"</td>
	</tr>
	<tr>
		<td>"_site "</td>
		<td>"一旦 Jekyll 完成转换，就会将生成的页面放在这里（默认）。最好将这个目录放进你的 .gitignore 文件中。"</td>
	</tr>
	<tr>
		<td>"index.html and other HTML, Markdown, Textile files"</td>
		<td>"如果这些文件中包含 YAML 头信息 部分，Jekyll 就会自动将它们进行转换。当然，其他的如 .html， .markdown，  .md，或者 .textile 等在你的站点根目录下或者不是以上提到的目录中的文件也会被转换。"</td>
	</tr>
	<tr>
		<td>"Other Files/Folders"</td>
		<td>"其他一些未被提及的目录和文件如  css 还有 images 文件夹， favicon.ico 等文件都将被完全拷贝到生成的 site 中。"</td>
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
