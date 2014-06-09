---
layout: post
title: Spring MVC PK Struts2
tags: spring web
---

{{ page.title }}
================

我们用struts2时采用的传统的配置文件的方式，并没有使用传说中的0配置。spring3 mvc可以认为已经100%零配置了（除了配置spring mvc-servlet.xml外）。

----------

Spring MVC和Struts2的区别：
 1. 机制：spring mvc的入口是servlet，而struts2是filter（这里要指出，filter和servlet是不同的。以前认为filter是servlet的一种特殊），这样就导致了二者的机制不同，这里就牵涉到servlet和filter的区别了。
 2. 性能：spring会稍微比struts快。spring mvc是基于方法的设计，而sturts是基于类，每次发一次请求都会实例一个action，每个action都会被注入属性，而spring基于方法，粒度更细，但要小心把握像在servlet控制数据一样。spring3 mvc是方法级别的拦截，拦截到方法后根据参数上的注解，把request数据注入进去，在spring3 mvc中，一个方法对应一个request上下文。而struts2框架是类级别的拦截，每次来了请求就创建一个Action，然后调用setter getter方法把request中的数据注入；struts2实际上是通过setter getter方法与request打交道的；struts2中，一个Action对象对应一个request上下文。
 3. 参数传递：struts是在接受参数的时候，可以用属性来接受参数，这就说明参数是让多个方法共享的。
 4. 设计思想上：struts更加符合oop的编程思想， spring就比较谨慎，在servlet上扩展。
 5. intercepter的实现机制：struts有以自己的interceptor机制，spring mvc用的是独立的AOP方式。这样导致struts的配置文件量还是比spring mvc大，虽然struts的配置能继承，所以我觉得论使用上来讲，spring mvc使用更加简洁，开发效率Spring MVC确实比struts2高。spring mvc是方法级别的拦截，一个方法对应一个request上下文，而方法同时又跟一个url对应，所以说从架构本身上spring3 mvc就容易实现restful url。struts2是类级别的拦截，一个类对应一个request上下文；实现restful url要费劲，因为struts2 action的一个方法可以对应一个url；而其类属性却被所有方法共享，这也就无法用注解或其他方式标识其所属方法了。spring3 mvc的方法之间基本上独立的，独享request response数据，请求数据通过参数获取，处理结果通过ModelMap交回给框架方法之间不共享变量，而struts2搞的就比较乱，虽然方法之间也是独立的，但其所有Action变量是共享的，这不会影响程序运行，却给我们编码，读程序时带来麻烦。
 6. spring3 mvc的验证也是一个亮点，支持JSR303，
 7. spring3 mvc处理ajax的请求更是方便，只需一个注解@ResponseBody ，然后直接返回响应文本即可。送上一段代码： 

    @RequestMapping(value="/whitelists")
    public String index(ModelMap map) {
    Account account = accountManager.getByDigitId(SecurityContextHolder.get().getDigitId());
    List<Group> groupList = groupManager.findAllGroup(account.getId());
    map.put("account", account);
    map.put("groupList", groupList);
    return "/group/group-index";
    }
    
    // @ResponseBody ajax响应，处理Ajax请求也很方便
    @RequestMapping(value="/whitelist/{whiteListId}/del")
    @ResponseBody
    public String delete(@PathVariable Integer whiteListId) {
    whiteListManager.deleteWhiteList(whiteListId);
    return "success";
    }
> 什么是JSR-303
> JSR-303 是JAVA EE 6 中的一项子规范，叫做Bean Validation，官方参考实现是Hibernate
> Validator。  此实现与Hibernate ORM 没有任何关系。JSR 303 用于对Java Bean 中的字段的值进行验证。 
> 
> Spring MVC 3.x之中也大力支持 JSR-303，可以在控制器中对表单提交的数据方便地验证。

> 什么是RESTful架构：
> (1)每一个URI代表一种资源；
> (2)客户端和服务器之间，传递这种资源的某种表现层；
> (3)客户端通过四个HTTP动词，对服务器端资源进行操作，实现"表现层状态转化"。

阮一峰理解RESTful架构:<http://www.ruanyifeng.com/blog/2011/09/restful.html>