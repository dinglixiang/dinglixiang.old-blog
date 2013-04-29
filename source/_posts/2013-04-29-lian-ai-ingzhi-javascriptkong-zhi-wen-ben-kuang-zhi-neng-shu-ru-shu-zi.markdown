---
layout: post
title: "恋爱ing之Javascript控制文本框只能输入数字"
date: 2013-04-29 15:30
comments: true
categories: 恋爱ing
---
>项目github地址：[恋爱ing ](https://github.com/dinglixiang/Shopping)

>bootstrap地址：[Bootstrap](http://xiemin.me/bootstrap-2.3.0/)


在填写如商品价格时，我们需要加入一些限制，如只能输入数字与小数点的限制。

◆ Javascript代码 

    <input   
    onkeypress = "return event.keyCode>=48&&event.keyCode<=57||        event.keyCode==46"   
    onpaste = "return !clipboardData.getData('text').match(/\D/)"   
    ondragenter = "return false"   
    style = "ime-mode:Disabled"   
    />   

说明： 

1.只能输入0到9和小数点 

2.只能粘贴数字 

3.不能拖动内容进来 

4.禁止使用输入法 

上面代码出处：<http://www.cnblogs.com/cloudgamer/articles/1138136.html> 

但是在上述代码的限制中，我是可以添加 N 多个小数点的，并不能完全满足我的需求。

将其改进的代码如下：

◆ **只能输入数字和一个点，且输入的第一个字符不能为点，可按退格键删除数字或点**

    <script type ="text/javascript " >
            function vailFloatNumberPerfect(evnt,obj){
             evnt=evnt||window.event;
             var keyCode=window.event?evnt.keyCode:evnt.which;
             if((obj.value.length==0 || obj.value.indexOf(".")!=-1) && keyCode==46) return false;
             return keyCode>=48&&keyCode<=57||keyCode==46||keyCode==8;
            }
    </script>


使用：

    <input   
    onkeypress = "return vaildFloatNumberPerfect(event,this) "   
    onpaste = "return !clipboardData.getData('text').match(/\D/) "   
    ondragenter = "return false "   
    style = "ime-mode:Disabled "   
    /> 

如：[新建产品时的价格](https://github.com/dinglixiang/Shopping/blob/master/web/NewProduct.jsp)

参考自： <http://www.denghuafeng.com/post-109.html>