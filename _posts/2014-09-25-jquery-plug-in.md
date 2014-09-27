---
layout: blog
title: jQuery插件的开发
categories: [jquery]
logo: jquery.png 
tags: [jquery,plug-in]
---


[jQuery](http://jquery.com/)单单使用的话看着它的[API](http://www.sd131.com/chm/jquery1.7.2.html)，还是能很好的运用它的。但是我们日常工作中不可能就用它的单个功能去完成很多复杂而且带有重复性的工作。
比如我工作中常要碰到的`滑动`,`tab切换`,`弹窗`等，我们就分别使用了[bxslider](http://www.bxslider.com/),[idTabs](http://www.sunsean.com/idTabs/),[simplemodal](http://www.ericmmartin.com/projects/simplemodal/)等jquery插件，极大程度上的使工作的重复性降低。

JQuery的插件开发推荐观看[这篇](http://www.iteye.com/topic/545971),写的完整和全面。

我只有在使用的时候才去观看相对应的文档，然后自己的技术能完成工作中的任务。下面我会写下我在工作中使用的jQuery的写法。因为工作的关系常用[seajs](http://seajs.org/docs/)来写对应功能的插件或者说是模块。在以后的文章中我会写下我所运用到的`seajs`功能。

>做着做着你就会使它了
>
>用着用着你就爱上它了

##jQuery插件开发常用写法
jQuery插件的开发包括两种：

- 方法一: `jquery.extend(object);` 给jquery类本身，添加方法
- 方法二：`jquery.fn.extend(object);` 给jquery对象添加方法

###jquery.extend(object)
例子：
{% highlight  javascript %}
$(document).ready(function($){
    var total = 0;
    $.sum=function(array){
        $.each(array,function(index,value){
            value = $.trim(value);
            value = parseFloat(value) || 0;
            total+=value;
        })
        return total;   
    } 
})
{% endhighlight %}

用法：
{% highlight  javascript %}
var arr=[1,2,3];
$.sum(arr);          //6
{% endhighlight %}


###jquery.fn.extend(object)
`jquery.fn==jquery.prototype`

例子：
{% highlight  javascript %}
var defaults={
           line: 1,
           speed: 2500,
           onSliderLoad:function(){},
           onSlideAfter:function(){}
 }
(function($){
   $.fn.extend({
       Scroll:function(opt,callback){
          var  Scroll={};
          Scroll= $.extend({}, defaults,opt);
          var _this = this.eq(0).find("ul:first");
         ...等扩展
    }
   }) 
})(jQuery);
{% endhighlight %}

seajs 改写
{% highlight  javascript %}
require("./xx.js")($)

return function($){     //return 可以换成exports
    $.fn.Scroll=function(options){
        var defaults={}
    }
}
{% endhighlight %}


运用
{% highlight  javascript %}
$("#....").Scroll({..});    //需要jquery对象 在代码中this指代jquery对象
{% endhighlight %}

