---
layout: post
title: "恋爱ing之购物车实现"
date: 2013-04-27 13:52
comments: true
categories: 恋爱ing
---
>项目github地址：[恋爱ing ](https://github.com/dinglixiang/Shopping)

>bootstrap地址：[Bootstrap](http://xiemin.me/bootstrap-2.3.0/)

***Before：界面引入bootstrap。***


用JSP的`Session`机制就可以让你拥有一个功能强大购物车程序，是不是很诱人呢？赶紧开始我们的程序吧！

**1.JSP Session 机制购物车之一构建的商品类**

◆写一个Product类，并定义商品的各个属性，返回商品属性的方法

◆[Product.java](https://github.com/dinglixiang/Shopping/blob/master/src/java/pack/Product.java)


    package pack;

    import java.util.*;
    public class Product {
    
    private int id,sales;//商品的id与销量
    private float price;  //商品的价格
    private String name,describe;//商品的名称与具体描述信息
    
    public Product(){
        id=0;
        sales=0;
        price=0;
        name=null;
        describe=null;
    }
    
    public Product(int id,String name,float price,String describe,int sales){
        this.id=id;
        this.name=name;
        this.price=price;
        this.describe=describe;
        this.sales=sales;
    }
    ...//封装字段  
    
    }

 
**2.JSP Session 机制购物车之二购物车实现**

◆在JavaBean中定义按照产品id查询出产品信息的方法（此方法用处很多）[FindProductById（int id）](https://github.com/dinglixiang/Shopping/blob/master/src/java/pack/FlowerBean.java)：
 
SQL语句：`String strsql="select * from products where product_id="+id;`
            

◆然后建立Product(商品)对象goods，并建立建立ArrayList对象bills

◆通过ArrayList对象的方法add()将商品对象添加到ArrayList对象bills中

◆由于ArrayList对象是具有添加和删除成员的方法，从而实现多个商品存储管理于ArrayList对象

◆将ArrayList对象bills存储于session对象当中，实现购物车功能

◆[MyCar.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/MyCar.jsp)
 
 
◆通过JavaBean调用FindProductById 方法，
在MyCar.jsp的`<head></head>` 标签中添加：

`<jsp:useBean id="flower" scope="application" class="pack.FlowerBean"/>`

◆获取参数信息：

    int id=Integer.parseInt(request.getParameter("id")); 
    Product tmp=flower.FindProductById(id);  
    String name=tmp.getName();
    int sales=tmp.getSales();
    String describe=tmp.getDescribe();
    float price=tmp.getPrice();

◆建立商品对象和ArrayList对象

    Product goods=new Product(id,name,price,describe,sales);
    ArrayList bills=null;

◆如果session中从未写入过，则将建立的商品对象添加到ArrayList对象当中，并写入 session

    if((ArrayList)session.getAttribute("car")==null)  
    {  
      bills = new ArrayList();  
      bills.add(goods);  
      session.setAttribute("car",bills);  
      response.sendRedirect("flowers.jsp");  
    }

◆如果ArrayList 对象不为空，则判断购入商品是否已经存在于车中,

    else 
    {  
     bills=(ArrayList)session.getAttribute("car");
     Iterator iter=bills.iterator();
      for(int i=0;i<bills.size();i++){
           Product p1=(Product)bills.get(i);
◆如果购入商品已经存在，则打印输入提示信息

           if(p1.getId()==goods.getId())
           {
               out.println("<script language=javascript>alert('已购买！');history.go(-1)</script>");
                return;
            }
        }

◆如果购入商品不存在，则直接将商品添加到ArrayList对象当中，并写入 session

        bills.add(goods);
        response.sendRedirect("flowers.jsp");
    }


**3.JSP Session 机制购物车之三删除商品**

◆对购物车中的商品进行删除操作

◆[removeGoods.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/removeGoods.jsp)


◆获取参数信息

    int id=Integer.parseInt(request.getParameter("id"));
       Product tmp=flower.FindProductById(id);  
       String name=tmp.getName();
       int sales=tmp.getSales();
       String describe=tmp.getDescribe();
       float price=tmp.getPrice();
◆创建符合条件参数要删除的商品对象

    Product goods=new Product(id,name,price,describe,sales);
         
◆获取session 中存储的ArrayList对象

    ArrayList products=(ArrayList)session.getAttribute("car"); 
    Iterator iter=products.iterator(); 

◆遍历ArrayList对象，并将ArrayList对象中的元素和创建的符合参数条件要删除的商品进行比较

    while(iter.hasNext()){
            Product p=(Product)iter.next();
            ◆查询是否有ArrayList对象中的元素与要删除的商品相同
            if(p.getId()==goods.getId()){
                int index=products.indexOf(p);
                products.remove(index);  //删除
                session.setAttribute("car",products); 
                response.sendRedirect("Cart.jsp"); 
                return;
            }
        }


**4.JSP Session 机制购物车之四清空购物车**

在购买完商品的时候，我们需要清空购物车session中的数据，如下：

`session.removeAttribute("car");`

 
JSP Session 机制购物车是不是使你眼睛豁然一亮的感觉呢？赶紧开始吧，JSP Session机制的使用期待你的尝试。