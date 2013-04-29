---
layout: post
title: "恋爱ing之购买商品销量增加"
date: 2013-04-27 14:43
comments: true
categories: 恋爱ing
---
>项目github地址：[恋爱ing ](https://github.com/dinglixiang/Shopping)

>bootstrap地址：[Bootstrap](http://xiemin.me/bootstrap-2.3.0/)

***Before：界面引入bootstrap。***

购买商品，不可避免的有销量这么一说。

◆本项目中在点击商品加入购物车的同时，我也通过`session`将所购买的商品的数量存放起来。

◆[MyCar.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/MyCar.jsp)

    //加入小车时传递的参数
    int id=Integer.parseInt(request.getParameter("id"));
    String count=request.getParameter("count");
    //设置session，以为可能购买商品的种类不是单一的，所以通过 "count"+id 来区分哪种商品所购买的数量
    session.setAttribute("count"+id,count);

**1.在购物车页面，也要通过数量计算商品的总价。**

首先定义一个总价的变量：
    float totalprice=0;

此处有循环输出，具体参考 Cart.jsp文件。
    //获取到购物车中商品的购买数量
    String count=(String)session.getAttribute("count"+(p.getId()));                                
    int cnt=Integer.parseInt(count);

在循环每个购物车的session时，计算总价：
    totalprice+=cnt*(p.getPrice()); 

最后在循环之外将总价显示出来。

**2.购买完成之后，商品的销量要增加。**

在订单信息页面（[OrderInfo.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/OrderInfo.jsp)）,循环过程中更新商品的销量。

    //获取属于该商品的购买数量
    String count=(String)session.getAttribute("count"+(p.getId()));
    int cnt=Integer.parseInt(count);
    //更新数据库中的销量信息
    product.UpdateSalesById(p.getId(),p.getSales(),cnt);

同之前调用FindProductById一样，此时调用的[UpdateSalesById方法](https://github.com/dinglixiang/Shopping/blob/master/src/java/pack/FlowerBean.java)也是通过JavaBean调用。


至此，商品销量的更新完成了。