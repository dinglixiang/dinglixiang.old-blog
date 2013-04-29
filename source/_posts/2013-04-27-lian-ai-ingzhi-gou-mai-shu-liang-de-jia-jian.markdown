---
layout: post
title: "恋爱ing之购买数量的加减"
date: 2013-04-27 14:52
comments: true
categories: 恋爱ing
---
>项目github地址：[恋爱ing ](https://github.com/dinglixiang/Shopping)

>bootstrap地址：[Bootstrap](http://xiemin.me/bootstrap-2.3.0/)

***Before：界面引入bootstrap。***

通过js实现购买产品的数量的加减

◆[flowers.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/flowers.jsp)

jsp加减样式：

    <input type="button" class="btn" value="-" onclick="minus(<%=p.getId()%>)">
    <input type="text" class="span1"  value="1" id="<%=p.getId() %>">
    <input type="button"  class="btn" value="+" onclick="plus(<%=p.getId()%>)">   

其中`p.getId()`是在页面展示产品时，循环产品的ArrayList获取的产品的`id`.

在点击`-`、`+`的按钮时，调用`minus`和`plus`的方法，且此方法将产品的`id`作为参数传递。

    <script type="text/javascript">
    function minus(id)
    {
    var count = document.getElementById(id).value;         
    document.getElementById(id).value = count-1;
    }
    </script>

    <script type="text/javascript">
    function plus(id)
    {
    var number=document.getElementById(id).value;                                      
    var cont=parseInt(number)+1;
    document.getElementById(id).value = cont;
    }
    </script>

在此简单说下为什么要用产品的id作为text的id，即此句。

`<input type="text" class="span1"  value="1" id="<%=p.getId() %>">`

  其实最开始，我实现数量的加减的时候，id是一个字符串，是不变的，在调用js的方法时，通过计算加减1，但是显示的位置是不对的，总是在第一个产品的数量text框中。后来发现，我在循环输出产品信息的时候，每个产品都有一个数量的text框，而且他们的id名称都是相同的，通过 `document.getElementById(id).value = cont; `改变文本框value值的时候，也就只能改变第一个产品的数量text文本框中的值。所以，后来就采用了一个动态的`id`作为传递的值。

  OK，至此，数量的加减操作已经完成了，可以将此值传递到下一个页面进行商品总价的计算了。