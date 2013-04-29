---
layout: post
title: "恋爱ing之返回顶部、底部"
date: 2013-04-27 15:10
comments: true
categories: 恋爱ing
---
>项目github地址：[恋爱ing ](https://github.com/dinglixiang/Shopping)

>bootstrap地址：[Bootstrap](http://xiemin.me/bootstrap-2.3.0/)


当页面信息过多时，为方便信息的浏览，人性化操作，特加入返回顶部、底部功能。

通过网上搜索，找到如下方法。
以[FlowerDetails.jsp](https://github.com/dinglixiang/Shopping/blob/master/web/FlowerDetails.jsp)为例。

**1.在`<head></head>`标签中加入如下js脚本，并引入[js文件](https://github.com/dinglixiang/Shopping/tree/master/web)：**

    <script type="text/javascript" src="jquery-1.4.1.js"></script>
    <style type="text/css">
        .go{width:47px;height:65px;position:fixed;_position:absolute;_top:expression(eval(document.documentElement.scrollTop+document.documentElement.clientHeight-this.offsetHeight-(parseInt(this.currentStyle.marginTop,10)||200)-(parseInt(this.currentStyle.marginBottom,10)||0)));right:20px;bottom:30%; background-color: lightgoldenrodyellow; background-repeat:no-repeat;}
        .go a{text-indent:999em;width:37px;margin:5px;border:0;overflow:hidden;float:left; cursor:pointer;}
        .go .top{background-position:0 0px;height:22px;background-image: url(./images/a.jpg);}
        .go .feedback{background-position:0 -22px;height:32px}
        .go .bottom{background-position:0 -55px;height:22px;background-image: url(./images/a.jpg);}
        .go .top:hover{background-position:-38px -0px}
        .go .feedback:hover{background-position:-38px -22px }
        .go .bottom:hover{background-position:-38px -55px}
        </style>
        <script type="text/javascript">
            $(function () {

                $(".top").click(//定义返回顶部点击向上滚动的动画
                function () {
                    $('html,body').animate({ scrollTop: 0 }, 700);
                });
                $(".bottom").click(//定义返回顶部点击向上滚动的动画
                function () {
                    $('html,body').animate({ scrollTop: document.body.clientHeight }, 700);

                });

            })
    </script>


**2.在`</body>`标签之前加入如下代码：**

    <div class="go">
      <a title="返回顶部" class="top"></a>
      <a title="返回底部" class="bottom" ></a>
    </div>

最后，页面信息过多时，即可查看效果。