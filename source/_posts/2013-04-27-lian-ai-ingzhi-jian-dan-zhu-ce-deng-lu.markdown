---
layout: post
title: "恋爱ing之简单注册登录"
date: 2013-04-27 13:27
comments: true
categories: 恋爱ing
---
>项目github地址：[恋爱ing ](https://github.com/dinglixiang/Shopping)

>bootstrap地址：[Bootstrap](http://xiemin.me/bootstrap-2.3.0/)

***Before：界面引入bootstrap。***

在本次作业项目中，用户的注册、登录就是简单的对数据库的数据进行插入与读取等操作。

1.[用户注册页面](https://github.com/dinglixiang/Shopping/blob/master/web/Register.jsp):Register.jsp

    <form class="form-signin" method="post" action="RegisterUser.jsp">
    <h2>注册</h2>
     <input type="text" class="input-block-level" placeholder="Email address" name="email">
     <input type="password" class="input-block-level" placeholder="Password" name="password">
     <input type="password" class="input-block-level" placeholder="Confirm Password" name="confirmpassword">
     <button class="btn btn-large btn-primary" type="submit">Sign up</button>
    </form>



2.这里通过`javaBean`调用了`insertRegisterData()`方法.

在`<head></head>`标签中加入：

    <jsp:useBean id="register" scope="application" class="pack.RegisterBean"/>
    <jsp:setProperty name="register" property="*"/>

然后在RegisterUser.jsp中[处理注册页面传递过来的数据](https://github.com/dinglixiang/Shopping/blob/master/web/RegisterUser.jsp)

在[javaBean](https://github.com/dinglixiang/Shopping/blob/master/src/java/pack/RegisterBean.java)中定义`insertRegisterData()`方法；

此时注册的流程就完成了。

3.登录就是将数据库数据读取出来并进行比较，在这就不多说了。

可参考：
[登录界面](https://github.com/dinglixiang/Shopping/blob/master/web/Login.jsp) |
[登录验证](https://github.com/dinglixiang/Shopping/blob/master/web/LoginValidate.jsp) |      	[登录LoginBean](https://github.com/dinglixiang/Shopping/blob/master/src/java/pack/LoginBean.java).
