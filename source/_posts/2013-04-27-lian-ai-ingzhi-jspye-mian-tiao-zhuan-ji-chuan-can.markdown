---
layout: post
title: "恋爱ing之jsp页面跳转及传参"
date: 2013-04-27 14:24
comments: true
categories: 恋爱ing
---
>项目github地址：[恋爱ing ](https://github.com/dinglixiang/Shopping)

>bootstrap地址：[Bootstrap](http://xiemin.me/bootstrap-2.3.0/)

***Before：界面引入bootstrap。***

**1.首先说下jsp页面跳转的一个小技巧**

`<a target=main onclick ="javascript:history.go(-1);">返回继续</a>`

返回到之前浏览的页面。

**2.其次说下本项目jsp页面中最常使用的页面跳转及传参方法**

以[flowers.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/flowers.jsp)中的加入小车为例

    <input class="btn btn-info" value="加入小车" type="button" onclick="{window.location.href='MyCar.jsp?id=<%=p.getId()%>&count='+document.getElementById(<%=p.getId()%>).value;}">

通过`onlick`事件传递参数，内容格式为：`onclick="{window.location.href='跳转页面.jsp'}"`

需要传参的话，格式为：

`window.location.href='跳转页面.jsp?参数名1=（要传递的参数）&参数名2=（要传递的参数)'`

在跳转的页面中可通过如下方式获取传递过来的参数：

    request.getParameter("参数名1")；
    request.getParameter("参数名2")；

具体代码可参考[MyCar.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/MyCar.jsp)。


**3jsp 页面跳转的几种方法**

跳转的方法网上一搜，到处都是的，但是还是要记录在我的开发过程中。


*(1). RequestDispatcher.forward()*

　　在服务器端起作用,当使用forward()时,Servlet engine传递HTTP请求从当前的Servlet或者是JSP到另外的一个Servlet、JSP 或普通HTML文件,也即你的form提交至a.jsp,在a.jsp用到了forward()重定向至b.jsp,此时form提交的所有信息在 b.jsp都可以获得,参数自动传递.

  但forward()无法重定向至有frame的jsp文件,可以重定向至有frame的html文件,同时forward()无法在后面带参数传递,比如servlet?name=frank,这样不行,可以程序内通过response.setAttribute("name",name)来传至下一个页面。

重定向后浏览器地址栏URL不变。

　　例：在servlet中进行重定向

    public void doPost(HttpServletRequest request,HttpServletResponse response) throws ServletException,IOException{
    response.setContentType("text/html; charset=gb2312");
    ServletContext sc = getServletContext();
    RequestDispatcher rd = null;
    rd = sc.getRequestDispatcher("/index.jsp"); //定向的页面
    rd.forward(request, response);
    }

通常在servlet中使用，不在jsp中使用。

*(2). response.sendRedirect()*

  是在用户的浏览器端工作,sendRedirect()可以带参数传递,比如servlet?name=frank传至下个页面,同时它可以重定向至不同的主机上,sendRedirect()可以重定向有frame.的jsp文件.

重定向后在浏览器地址栏上会出现重定向页面的URL

*ps:这也是本项目中用到最多的页面跳转方法*。

*(3). ＜jsp:forward page="" /＞*

  它的底层部分是由RequestDispatcher来实现的，因此它带有RequestDispatcher.forward()方法的印记。

如果在之前有很多输出,前面的输出已使缓冲区满,将自动输出到客户端,那么该语句将不起作用,这一点应该特别注意。

*(4). 修改HTTP header的Location属性来重定向*

  通过设置直接修改地址栏来实现页面的重定向。jsp文件代码如下：
    response.setStatus(HttpServletResponse.SC_MOVED_PERMANENTLY);
    String newLocn = "/newpath/jsa.jsp";
    response.setHeader("Location",newLocn);


*(5). JSP中实现在某页面停留若干秒后,自动重定向到另一页面*

　　在html文件中，下面的代码：

　　`＜meta http-equiv="refresh" content="300; url=target.jsp"＞`

　　它的含义：在5分钟之后正在浏览的页面将会自动变为target.html这一页。代码中300为刷新的延迟时间，以秒为单位。targer.html为你想转向的目标页,若为本页则为自动刷新本页。

　　由上可知，可以通过setHeader来实现某页面停留若干秒后,自动重定向到另一页面。代码：

    String content=stayTime+";URL="+URL;
    response.setHeader("REFRESH",content);

另外要注意：它不能改变浏览器地址，刷新的话会导致重复提交.

ps:*本项目的注册等页面([RegisterUser.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/RegisterUser.jsp))有一点点使用。*
