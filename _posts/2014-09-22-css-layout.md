---
layout: blog
title: css布局练习
categories: [css]
logo: css.png 
tags: [css,layout,box]
---

ccs样式的运用应该算在前端工作中首先会碰到的问题吧，工作中我也是从css和html
慢慢的学起的。我工作初经过一个多月的[w3c](http://www.w3school.com.cn/)的摸索中 
感觉自己对布局已经有了一定的了解。后来在[这篇教材](http://zh.learnlayout.com/index.html)
的启迪下，发现了很多自己不知道的，非常适合初学者观看。下面我将常用的3种类布局样式
进行基本的基础知识回顾。

##display属性:
每个元素都有一个默认的display值，这与元素的类型有关。对多数元素它们的
默认值通常是block或inline

- 一个block元素通常是块元素（`<h1>~<h6>`,`<p>`,`<ul>`,`<li>`....）
  - 特点1：会相互堆叠在一起沿页面向下排列，每个元素占一行
  - 特点2：块元素盒子会扩展到与父元素同宽

- 一个inline元素通常是行内元素（`<a>`,`<img>`,`<em>`,`<strong>`....）
  - 特点1：在行内元素相互并列，在空间不足的情况下会折到下一行
  - 特点2：行内元素盒子会**收缩包裹**其内容，并且会尽可能抱紧

###block
`div`为一个标准的块级元素。一个块级元素会新开始一行并且尽可能撑满容器。
其他包括`p`，`from`和HTML5中的新元素：`header`，`footer`，`section`等等。

###inline
`span`是一个标准的行内元素。一个行内元素可以在段落中`<span>像这样</span>`	 
包裹一些文字而不会打乱段落的布局。a元素是最常用的行内元素。
*高，行高及顶和底边距不可改变；

###none
一些特殊的元素的默认`display`值是它，例如`script`。 它和`visibility`属性不一样。把`display`设置成`none`不会保留元素本该显示的空间。但是`visibility:hidden;`还会保留。

###inline-block
`inline-block`的元素即具有`block`元素可以设置宽高的特性，同时又具有`inline`
元素默认不换行的特性。比如` inline-block `元素也可以设置` vertical-align `属性
简而言之：
> `inline-block `后的元素就是一个格式化为行内元素的块容器( `Block container` )

推荐观看[inline-block 前世今生](http://ued.taobao.org/blog/2012/08/inline-block/)讲的很好，需要了解的可以去看下，但是代码的话不用很容易忘记。


##float属性
说要浮动我想大家首先会想到的是浮动所引发的总总问题，然后我们就需要去清除浮动。
这里要介绍下的[那些年我们一起清除过的浮动](http://www.iyunlu.com/view/css-xhtml/55.html)
看过这篇我想你一定会对清除浮动有很深的了解。

由Nicolas Gallagher 大湿提出来的清除浮动的方法：

{% highlight css %}
/*---去除浮动--*/
.clearfix:after {
    content: ".";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
.clearfix {
    zoom: 1;
}
{% endhighlight %}


##position属性

默认值。任意`position:static;`的元素不会被特殊定位。
{% highlight css %}  	 
.static {
    position: static;
}
{% endhighlight %}


`relative`表现的和`static`一样，除非你添加了一些额外的属性。在一个相对定位（position属性的值为relative）的元素上设置top，right，bottom和left属性会使其偏离其正常位置。其他的元素则不会调整位置来弥补它偏离后剩下的空隙。
{% highlight css %}  	   
.relative1 {
    position: relative;
}
.relative2 {
	position: relative;
	top: -20px;
	left: 20px;
	background-color:white;
	width: 500px;
}
{% endhighlight %}

  

`absolute`与`fixed`的表现类似，除了它不是相对于视窗而是相对于最近的“positioned”祖先元素。
如果绝对定位（position属性的值为absolute）的元素没有”position“祖先元素，那么它是相对于文档的body元素，并且它会随着页面滚动而移动。
{% highlight css %}  	
.relative {
  position: relative;
  width: 600px;
  height: 400px;
}
.absolute {
  position: absolute;
  top: 120px;
  right: 0;
  width: 300px;
  height: 200px;
}
{% endhighlight %}



