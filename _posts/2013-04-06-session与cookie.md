---
layout: post
title: session与cookie
tags: java
---

{{ page.title }}
================

Cookie的概念
------------

Cookie是浏览器（User Agent）访问一些网站后，这些网站存放在客户端的一组数据，用于使网站等跟踪用户，实现用户自定义功能。

Cookie的Domain和Path属性标识了这个Cookie是哪一个网站发送给浏览器的；Cookie的Expires属性标识了Cookie的有效时间，当Cookie的有效时间过了之后，这些数据就被自动删除了。

如果不设置过期时间，则表示这个Cookie生命周期为浏览器会话期间，只要关闭浏览器窗口，Cookie就消失了。这种生命期为浏览会话期的Cookie 被称为会话Cookie。会话Cookie一般不保存在硬盘上而是保存在内存里。session的实现机制里面除了已经介绍了会话cookie（session cookie），还有平常所说的cookie主要指的是另一类cookie——持久cookie（persistent cookies）。持久cookie是指存放于客户端硬盘中的 cookie信息（设置了一定的有效期限），当用户访问某网站时，浏览器就会在本地硬盘上查找与该网站相关联的cookie。如果该cookie 存在，浏览器就将它与页面请求一起通过HTTP报头信息发送到您的站点，然后在系统会比对cookie中各属性和值是否与存放在服务器端的信息一致，并根据比对结果确定用户为“初访者”或者“老客户”。

Session的概念
-------------

Session 是存放在服务器端的类似于HashTable结构（每一种Web开发技术的实现可能不一样，下文直接称之为HashTable）来存放用户数据，当浏览器 第一次发送请求时，服务器自动生成了一个HashTable和一个Session ID用来唯一标识这个HashTable，并将其通过响应发送到浏览器。当浏览器第二次发送请求，会将前一次服务器响应中的Session ID放在请求中一并发送到服务器上，服务器从请求中提取出Session ID，并和保存的所有Session ID进行对比，找到这个用户对应的HashTable。

一般情况下，服务器会在一定时间内（默认20分钟）保存这个 HashTable，过了时间限制，就会销毁这个HashTable。在销毁之前，程序员可以将用户的一些数据以Key和Value的形式暂时存放在这个 HashTable中。当然，也有使用数据库将这个HashTable序列化后保存起来的，这样的好处是没了时间的限制，坏处是随着时间的增加，这个数据 库会急速膨胀，特别是访问量增加的时候。一般还是采取前一种方式，以减轻服务器压力。

Session的客户端实现形式（即Session ID的保存方法）
------------------------------------------------

一般浏览器提供了三种方式来保存，还有一种是程序员使用HTML隐藏域的方式自定义实现：

[1] 使用Cookie来保存，这是最常见的方法，本文“记住我的登录状态”功能的实现正式基于这种方式的。服务器通过设置Cookie的方式将Session ID发送到浏览器。如果我们不设置这个过期时间，那么这个Cookie将不存放在硬盘上，当浏览器关闭的时候，Cookie就消失了，这个Session ID就丢失了(只放入内存，并不存在硬盘中)。如果我们设置这个时间为若干天之后，那么这个Cookie会保存在客户端硬盘中，即使浏览器关闭，这个值仍然存在，下次访问相应网站时，同 样会发送到服务器上。

[2] 使用URL附加信息的方式，也就是像我们经常看到JSP网站会有aaa.jsp?JSESSIONID=*一样的。这种方式和第一种方式里面不设置Cookie过期时间是一样的。

[3] 第三种方式是在页面表单里面增加隐藏域，这种方式实际上和第二种方式一样，只不过前者通过GET方式发送数据，后者使用POST方式发送数据。但是明显后者比较麻烦。

session共享
-----------

通常session cookie是不能跨窗口使用的，当你新开了一个浏览器窗口进入相同页面时，系统会赋予你一个新的sessionid，这样我们信息共享的目的就达不到了，此时我们可以先把sessionid保存在persistent cookie中，然后在新窗口中读出来，就可以得到上一个窗口SessionID了，这样通过session cookie和persistent cookie的结合我们就实现了跨窗口的session tracking（会话跟踪）。

还有一点需要注意，就是现在的浏览器好像趋向于多进程的session共享，即通过多个标签或页面打开多个进程访问同一网站时共享一个 session cookie，只有当浏览器被关闭时才会被清除，也就是你有可能在标签中关闭了该网站，但只要浏览器未被关闭并且在服务器端的session未失效前重新开启该网站，那么就还是使用原session进行浏览；而某些浏览器在打开多页面时也可能建立独立的session，IE8、Chrome默认都是共享 session的，在IE8中可以通过菜单栏中的文件->新建会话来建立独立session的浏览页面。

session生命周期
---------------

session什么时候被创建？

一个常见的错误是以为session在有客户端访问时就被创建，然而事实是直到某server端程序(如Servlet)调用HttpServletRequest.getSession(true)这样的语句时才会被创建。

session何时被删除？

session在下列情况下被删除：1．程序调用HttpSession.invalidate()；2．距离上一次收到客户端发送的session id时间间隔超过了session的最大有效时间；3．服务器进程被停止.

是否只要关闭浏览器，session就消失了？

程序一般都是在用户做log off的时候发个指令去删除session，然而浏览器从来不会主动在关闭之前通知服务器它将要被关闭，因此服务器根本不会有机会知道浏览器已经关闭。服务器会一直保留这个会话对象直到它处于非活动状态超过设定的间隔为止。
之所以会有这种错误的认识，是因为大部分session机制都使用会话cookie来保存session id，而关闭浏览器后这个session id就消失了，再次连接到服务器时也就无法找到原来的session。
如果服务器设置的cookie被保存到硬盘上，或者使用某种手段改写浏览器发出的HTTP请求报头，把原来的session id发送到服务器，则再次打开浏览器仍然能够找到原来的session。
恰恰是由于关闭浏览器不会导致session被删除，迫使服务器为session设置了一个失效时间，当距离客户上一次使用session的时间超过了这个失效时间时，服务器就可以认为客户端已经停止了活动，才会把session删除以节省存储空间。

这是一个很关键性的注意点，即session失效时间的设置，这里要分两方面来看：浏览器端和服务端。对于浏览器端而言，session与访问进程直接相关，当浏览器被关闭时，session也随之消失；而服务器端的session失效时间一般是人为设置的，目的是能定期地释放内存空间，减小服务器压力，一般的设置为当会话处于非活动状态达20或30分钟时清除该 session，所以浏览器端和服务端的session并非同时消失的，session的中断也并不一定意味着用户一定离开了该网站。目前Google Analytics和Omniture都定义当间隔30分钟没有动作时，算作一次访问结束，所以session的最后一步不只是离开，也有可能是静止、休眠或者发呆的状态。

#### 一些网址：

很全的session与cookie区别：<http://blog.csdn.net/macsnow/article/details/6893191>
session与cookie:<http://www.chinahtml.com/1007/128010707619425.html>
cookie:<http://blog.csdn.net/ghsau/article/details/20395681>


{% include references.md %}
{% include pictures.md %}
