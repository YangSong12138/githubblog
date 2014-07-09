---
layout: post
title: session与cookie
tags: java
---

{{ page.title }}
================

web.xml 的加载顺序是：context- param -> listener -> filter -> servlet 

三者区别
--------

1. Filter
实现javax.servlet.Filter接口，在web.xml中配置与标签指定使用哪个Filter实现类过滤哪些URL链接。只在web启动时进行初始化操作。

filter 流程是线性的， url传来之后，检查之后，可保持原来的流程继续向下执行，被下一个filter, servlet接收等，而servlet 处理之
后，不会继续向下传递。filter功能可用来保持流程继续按照原来的方式进行下去，或者主导流程，而servlet的功能主要用来主导流程。
特点：可以在响应之前修改Request和Response的头部，只能转发请求，不能直接发出响应。filter可用来进行字符编码的过滤，检测用户
是否登陆的过滤，禁止页面缓存等

2. Servlet
servlet 流程是短的，url传来之后，就对其进行处理，之后返回或转向到某一自己指定的页面。它主要用来在业务处理之前进行控制。

3. Listener
servlet,filter都是针对url之类的，而listener是针对对象的操作的，如session的创建，session.setAttribute的发生，在这样的事件发
生时做一些事情。

filter
------

Filter is an object which transform the request and response (header as well as content).
Servlet Filter is used for manipulating the request and response from client to the servlet, or to modify the request and response, or to audit and log. Filters are called on a per-request basis and listeners are not. Filters have access to request object and listeners don’t. Filters can perform many different types of functions. We’ll discuss examples of the italicized items in this paper:
Authentication-Blocking requests based on user identity.
Logging and auditing-Tracking users of a web application.
Image conversion-Scaling maps, and so on.
Data compression-Making downloads smaller.
Localization-Targeting the request and response to a particular locale.
XSL/T transformations of XML content-Targeting web application responses to more that one type of client.

filter功能，它使用户可以改变一个 request和修改一个response. Filter 不是一个servlet,它不能产生一个response,它能够在一个request到达servlet之前预处理request,也可以在离开 servlet时处理response.换种说法,filter其实是一个”servlet chaining”(servlet 链).

一个Filter包括：

1）、在servlet被调用之前截获;

2）、在servlet被调用之前检查servlet request;

3）、根据需要修改request头和request数据;

4）、根据需要修改response头和response数据;

5）、在servlet被调用之后截获.

listener
--------

You can monitor and react to events in a servlet’s life cycle by defining listener objects whose methods get invoked when life cycle events occur. Servlet Listener is used for listening various events inside a web containers, such as when you create a session, or place an attribute in a session or if you passivate and activate in another container, to manipulate these events you can configure listener in web.xml

它是基于观察者模式设计的，Listener 的设计对开发 Servlet 应用程序提供了一种快捷的手段，能够方便的从另一个纵向维度控制程序和数据。目前 Servlet 中提供了 5 种两类事件的观察者接口，

它们分别是：4 个 EventListeners 类型的，

ServletContextAttributeListener(application范围内的属性变化，把一个属性从application范围存入移除替换)、

ServletRequestAttributeListener（request范围内的属性变化）、

ServletRequestListener（用户请求初始化、销毁）、

HttpSessionAttributeListener（session范围内的属性变化） 

2 个 LifecycleListeners 类型的，

ServletContextListener（应用开始与销毁）、

HttpSessionListener（用户与服务器回话开始、创建、回话断开、销毁） 。

附：
struts2中的过滤器和拦截器的区别与联系：
　　(1)、拦截器是基于java反射机制的，而过滤器是基于函数回调的。
　　(2)、过滤器依赖与servlet容器，而拦截器不依赖与servlet容器。
　　(3)、拦截器只能对Action请求起作用，而过滤器则可以对几乎所有请求起作用。
　　(4)、拦截器可以访问Action上下文、值栈里的对象，而过滤器不能。
　　(5)、在Action的生命周期中，拦截器可以多次调用，而过滤器只能在容器初始化时被调用一次。


{% include references.md %}
{% include pictures.md %}
