---
layout: post
title: java之String的秘密
tags: java
---

{{ page.title }}
================

众所周知的秘密
--------------

String对象是不可修改的。你对他进行的任何修改字符序列的操作其实都是返回修建的String对象，所以它具有线程安全性，可以自由的实现共享。

String字面常量和常量池
----------------------

java通过String常量池共享String对象。

当String对象是编译时常量(String字面常量和String表达式)，就会去常量池中寻找相等的对象。否则，会在运行时创建String对象，并分配到堆里。

equals与==
----------

默认情况下，他们两个是完全等价的，比较的是对象的地址，因为调用他的对象大部分继承自Object类，不过你可以重写equals方法，String类的equals方法就是重写过，比较的对象内容。需要牢记的是重写equals()方法时，一定要重写hashcode()方法



运算符‘+’的秘密
---------------

当使用运算符‘+’连接字符串的时候，实际上是使用临时创建的StringBuilder对象来辅助完成的。因此，循环操作进行String对象连接操作时，应该直接使用StringBuilder。

但也有例外，但‘+’连接的两个操作数都是编译时常量时，则会在编译时计算字符串的值，就不会再到运行时创建的StringBuilder对象。

注意事项
--------

方法中形参的改变无法作用于实参，但可以通过引用来修改其成员变量来修改其值。

{% include references.md %}
{% include pictures.md %}
