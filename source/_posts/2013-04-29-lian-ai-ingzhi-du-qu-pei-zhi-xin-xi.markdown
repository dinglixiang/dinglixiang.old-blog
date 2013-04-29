---
layout: post
title: "恋爱ing之读取配置信息"
date: 2013-04-29 15:18
comments: true
categories: 恋爱ing
---
>项目github地址：[恋爱ing ](https://github.com/dinglixiang/Shopping)

>bootstrap地址：[Bootstrap](http://xiemin.me/bootstrap-2.3.0/)

***Before：界面引入bootstrap。***

在本项目中，为了方便快捷，我是将管理员的账号密码等信息放在配置文件`web.xml`中的。

如在[web.xml](https://github.com/dinglixiang/Shopping/blob/master/web/WEB-INF/web.xml)文件中，有以下配置信息：

    <context-param>
        <param-name>email</param-name>
        <param-value>admin@gmail.com</param-value>
    </context-param>

那么，怎样读取这个配置账号呢？

◆ 在jsp页面中，可以通过 `${initParam.email} `直接获取到配置文件的信息并显示在页面上，但是在管理员登录时，我们还要进行信息的比较。

如何在jsp 的<%  %>中获取配置信息呢？ 

我们可通过 `application.getInitParameter("email")` 来获取`web.xml`中的`email`的值，从而与登录界面传递的值进行比较验证。如：[AdminValidate.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/AdminValidate.jsp) 所示。