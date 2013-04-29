---
layout: post
title: "恋爱ing之商品搜索"
date: 2013-04-27 15:01
comments: true
categories: 恋爱ing
---
>项目github地址：[恋爱ing ](https://github.com/dinglixiang/Shopping)

>bootstrap地址：[Bootstrap](http://xiemin.me/bootstrap-2.3.0/)

***Before：界面引入bootstrap。***

本项目的搜索仅限于模糊搜索。

**1.搜索样式表单：**

◆[flowers.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/flowers.jsp)

    <form class="navbar-search pull-search" action="SearchResult.jsp">                                              
     <input type="text" class="search-query" name="condition">
     <button type="submit" class="btn" >搜索</button>
    </form>

**2.处理表单数据**
◆[SearchResult.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/SearchResult.jsp)，通过javaBean调用[SearchResult方法](https://github.com/dinglixiang/Shopping/blob/master/src/java/pack/FlowerBean.java),调用方法请参考前几篇blog。

    //接受搜索条件参数
    String condition=request.getParameter("condition");
    //通过javaBean调用搜索方法
    ArrayList flowers=flower.SearchResult(condition);
    //循环输出结果
    Iterator iter=flowers.iterator();
    ......此处省略

◆调用pack.FlowerBean.java中
[SearchResult方法](https://github.com/dinglixiang/Shopping/blob/master/src/java/pack/FlowerBean.java)

    //模糊查询的sql语句
    String strsql="select * from products where product_name like "+"'%"+condition+"%'";

OK，我就实现了这么一点模糊查询的功能了。后续可能会添加更加强大点的搜索~~~