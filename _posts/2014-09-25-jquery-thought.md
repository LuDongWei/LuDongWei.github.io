---
layout: blog
title: jQuery设计思想
categories: [jquery]
logo: jquery.png 
tags: [jquery,thougth]
---

[jQuery](http://jquery.com/)应该算是工作中最常用的javascript函数库。
配合和完善它的插件也不计其数。运用后能很大程度上的完成日常工作中70%的
任务要求（对我现在的工作来说）。

目前，互联网上最好的jQuery入门教材，是Rebecca Murphey写的《jQuery基础》（jQuery Fundamentals）。在Google里搜索"jQuery 培训"，此书排在第一位。jQuery官方团队已经同意，把此书作为官方教程的基础。

下面篇转自[阮一峰](http://www.ruanyifeng.com/blog/2011/07/jquery_fundamentals.html)
老师的译文。能在短时间里，掌握jQuery的所有方面（除了**ajax**和**插件开始**）


#jQuery设计思想
> 原文网址：http://jqfundamentals.com/book/
>
> 阮一峰 翻译整理

####一，选择网页元素（选择某个网页元素，然后对其进行某种操作）

css选择器：

{% highlight  javascript  %}
$(document)              //选择整个文档对象
$('#myId')               //选择ID为myId的网页元素
$('div.myClass')         //选择class为myClass的div元素
$('input[name=first]')   //选择name属性等于first的input元素
{% endhighlight %}

jQuery特有的表达式：

{% highlight  javascript  %}
$('a:first')             //选择网页中第一个a元素
$('tr:odd')              //选择表格的奇数行
$('#myForm :input')      //选择表单中的input元素
$('div:visible')         //选择可见的div元素
$('div:gt(2)')           //选择所有的div元素，除了前三个
$('div:animated')        //选择当前处于动画状态的div元素
{% endhighlight %}

####二,改变结果集 （提供各种强大的过滤器，对结果集进行筛选，缩小选择结果）

{% highlight  javascript  %}
$('div').has('p');           //选择包含p元素的div元素
$('div').not('.myClass');    //选择class不等于myClass的div元素
$('div').filter('.myClass'); //选择class等于myClass的div元素
$('div').first();            //选择第1个div元素
$('div').eq(6);              //选择第6个div元素
{% endhighlight %}	

在DOM树上的移动方法:

{% highlight  javascript  %}
$('div').next('p');         //选择div元素后面的第一个p元素
$('div').parent();          //选择div元素的父元素
$('div').closest('form');   //选择离div最近的那个form父元素
$('div').children();        //选择div的所有子元素
$('div').siblings();        //选择div的同级元素
{% endhighlight %}	

####三，链式操作 （对它进行一系列操作，并且操作可以连接在一起）

{% highlight  javascript  %}
$('div').find('h3').eq(2).html('hello');

分解开来
$('div')         //找到div元素
.find('h3')      //选择其中的h3元素
.eq(2)           //选择第3个元素
.html('hello');  //将它的内容改成helo
（原理在于每一步的JQuery，返回都是一个jQuery对象。）

.end()   //使得结果集可以后退一步
{% endhighlight %}	    

####四，元素的操作：取值和赋值 （一个函数来完成）

{% highlight  javascript  %}
$('h1').html();         //html()没有参数，表示取出h1的值
$('h1').html('hello');  //html()有参数Hello，表示对h1进行赋值
{% endhighlight %}		

常见的取值和赋值函数如下：

{% highlight  javascript  %}
.html()     //取出或设置html内容
.text()     //取出或设置text内容
.attr()     //取出或设置某个属性的值
.width()    //取出或设置某个元素的宽度
.height()   //取出或设置某个元素的高度
.val()      //取出某个表单元素的值
（如果结果集包含多个元素，那么赋值的时候，将对其所有的元素赋值；
  取值的时候，则是只取出第一个元素的值（.text()例外，取出所有元素的text内容））
{% endhighlight %}	
  
####五，元素的操作：移动 （一组方法是直接移动该元素，另一种方法是移动其他元素）

假定我们选择一个div元素，需要把它移动到p元素后面。

{% highlight  javascript  %}
第一种：把div元素移动到p元素后面  
$('div').insertAfter($('p'));
                                 
第二种：把p元素加到div元素前面
$('p').after($('div'));

区别：第一种返回div元素，第二种返回p元素
{% endhighlight %}	

这种模式的操作方法，一共有四对：

{% highlight  javascript  %}
.insertAfter()和.after():    //在现存元素的外部，从后面插入元素
.insertBefore()和.before():  //在现存元素的外部，从前面插入元素
.appendTo()和.append():      //在现存元素的内部，从后面插入元素
.prepenTo()和.prepend():     //在现存元素的内部，从前面插入元素
{% endhighlight %}	

####六，元素的操作：复制，删除和创建

{% highlight  javascript  %}
复制元素：.clone();
删除元素；.remove()和.detach();  //两者区别：前者不保留被删除元素事件，后者保留，
                                   有利于重新插入文档时使用。
清空元素：.empty();
创建元素：直接把新元素传入jQuery的构造函数：
          $('<p>Hello</p>');
　　      $('<li class="new">new list item</li>');
　　      $('ul').append('<li>list item</li>');
{% endhighlight %}	


####七：工具方法 （不必选择元素，就可以直接使用这些方法）
原理：工具方法-定义在JQuery构造函数上，即jQuery.method();
      操作元素-构造函数的prototype对象上的方法，即jQuery.prototype.method();

常见的工具方法有以下：

{% highlight  javascript  %}
$.trim()           //去除字符串两端的空格。
$.each()           //遍历一个数组或对象。
$.inArray()        //返回一个值在数组中的索引位置。如果改值不在数组中，则返回-1。
$.grep()           //返回数组中符合某种标准的元素。
$.extend()         //将多个对象，合并到第一个对象。
$.makeArray()      //将对象转化为数组。
$.type()           //判断对象的类别（函数对象，日期对象，数组对象，正则对象等等）。
$.isArray()        //判断某个参数是否为数组。
$.isEmptyObject()  //判断某个对象是否为空（不含有任何属性）。
$.isFunction()     //判断某个参数是否为函数。
$.isPlainobject()  //判断某个参数是否为用“{}”或“new object”建立的对象。
$.support()        //判断游览器是否支持某个特性。
{% endhighlight %}	


####八，事件操作 （事件直接绑定在网页元素上）


jQuery主要支持以下事件：

{% highlight  javascript  %}
.blur()            //表单元素失去焦点
.change()          //表单元素的值发生变化
.click()           //鼠标点击
.dblclick()        //鼠标双击
.focus()           //表单元素获得焦点
.focusin()         //子元素获得焦点
.focusout()        //子元素失去焦点
.hover()           //同时为mouseenter和mouseleave事件指定处理函数
.keydown()         //按下键盘（长时间按键，只返回一个事件）
.keypress()        //按下键盘（长时间按键，将返回多个事件）
.keyup()           //松开键盘
.load()            //元素加载完毕
.mousedown()       //按下鼠标
.mouseenter()      //鼠标进入（进入子元素不触发）
.mouseleave()      //鼠标离开（离开子元素不触发）
.mousemove()       //鼠标在元素内部移动
.mouseout()        //鼠标离开（离开子元素也触发）
.mouseover()       //鼠标进入（进入子元素也触发）
.mouseup()         //松开鼠标
.ready()           //DOM加载完成
.resize()          //游览器窗口的大小发生改变
.scroll()          //滚动条的位置发生变化
.select()          //用户选中文本框中的内容
.submit()          //用户递交表单
.toggle()          //根据鼠标点击的次数，依次运行多个函数
.unload()	       //用户离开页面
{% endhighlight %}	


以上事件在JQuery内部，都是.bind()的便捷方式。
（使用.bind()可以更灵活地控制事件）
{% highlight  javascript  %}
$('input').bind(
   'click change', //同时绑定click和change事件
   function(){
     alert('Hello');
   }
);
{% endhighlight %}	

有时，你只想让事件运行一次，可以使用.one()方法
{% highlight  javascript  %}
$('p').one('click',function(){
   alert('hello'); //只运行一次，以后的点击不会运行
});
{% endhighlight %}	

.unbind()用来解除事件绑定。
{% highlight  javascript  %}
$('p').unbind('click');
{% endhighlight %}

所有事件，都可以接受一个事件对象（event object）作参数
{% highlight  javascript  %}
$('p').click(function(e){
   alert(e.type);// 'click'
})
{% endhighlight %}

这个事件对象有一些很有用的属性和方法：

{% highlight  javascript  %}
event.pageX                //事件发生时，鼠标距离网页左上角的水平距离
event.pageY                //事件发生时，鼠标距离网页左上角的垂直距离
event.type                 //事件的类型（比如click）
event.which                //按下了哪一个键
event.data                 //在事件对象上绑定数据，然后传入事件处理函数
event.target()             //事件针对的网页元素
event.preventDefault()     //阻止事件的默认行为（比如点击链接，会自动打开新页面）
event.stopPropagation()    //停止事件向上层元素冒泡
{% endhighlight %}	

在事件处理函数中，可以用this关键字，返回事件针对的DOM元素：

{% highlight  javascript  %}
$('a').click(function(e){
    if($(this).attr('href').match('evil')){ //如果确定认为有害链接
	    e.preventDefault():            //阻止打开
		$(this).addClass('evil');      //加上表示有害的class
	}
})
{% endhighlight %}		

有两种方法，可以自动触发一个事件。一种是直接使用事件函数，另一种是使用
{% highlight  javascript  %}
.trigger()和.triggerHandler().
$('a').click();
$('a').trigger('click');
{% endhighlight %}		

####九，特殊效果
常用的特殊效果：

{% highlight  javascript  %}
.fadeIn()       //淡入
.fadeOut()      //淡出
.fadeTo()       //调整透明度
.hide()         //隐藏元素
.show()         //显示元素
.slideDown()    //向下展开
.slideUp()      //向上卷起
.slideToggle()  //依次展开或卷起某个元素
.toggle()       //依次展开或隐藏某个元素
{% endhighlight %}	

除了.show()和.hide(),所有其他特效默认执行时间都是400ms（毫秒），
但是你可以改变这个设置
{% highlight  javascript  %}
$('h1').fadeIn(300);     // 300毫秒内淡入
$('h1').fadeOut('slow'); // 缓慢地淡出
{% endhighlight %}		

执行特效后，可以指定摸个函数。
{% highlight  javascript  %}
$('p').fadeOut(300, function() { $(this).remove(); });
{% endhighlight %}	

更复杂的特效，可以.animate()自定义。
{% highlight  javascript  %}
$('div').animate(
   {
     left:'+=50',   //不断右移
	 opacity:0.25   //指定透明度
   }
   300，            //持续时间
   function()
   {alert('done!');}//回调函数
);
{% endhighlight %}	

.stop()和.delay()用来停止或延缓特效的执行。
$.fx.off如果设置为true，则关闭所有网页特效。




    