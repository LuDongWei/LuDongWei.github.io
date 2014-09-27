---
layout: blog
title: jQery的deferred对象
categories: [jquery]
logo: jquery.png 
tags: [jquery,deferred]
---

[jQuery](http://jquery.com/)的deferred对象应该算是不经常用到的jQuery对象吧。
在看过我前面写和转载的[jQuery设计思想](http://www.ludongwei.com/jquery/2014/09/25/jquery-thought.html)和[jQuery插件的开发](http://www.ludongwei.com/jquery/2014/09/25/jquery-plug-in.html)过后应该已经可以很自如的使用jQuery了。在你使用jquery的`ajax`的时候往往会使用回调函数`callback`来完成对应数据的输出。

常用ajax写法：
{% highlight javascript %}
function Ajax(url, data, callback) {
          $.ajax({
               type: "get",
               url: url,
               dataType: "jsonp",
               jsonp: "jsoncallback",
               data: data,
               success: function(json) {
                    callback && callback(json);
               }
          })
 }
{% endhighlight %}

但在使用的过程中会碰到一个小问题，如果你在`success`中写了别的方法
需要对数据进行多次的输出。这样原来的程序就会出现问题，输出的内容只能进行一次。只能把`ajax`方法再运行一遍才能解决问题。这是我们所不需要的。在此前提下我运用了`deferred`对象。

遇到的问题：
{% highlight javascript %}
Ajax('url',{},function(aa){
      //如果success进行多次数据的输出，这边只能接收一次。
})
{% endhighlight %}

解决方法使用`deferred`对象：
{% highlight javascript %}
function sJson(){
     var dfd = new $.Deferred();
     $.ajax({
        type:"GET",
        dataType: "jsonp",
        jsonp: "jsoncallback",
        success: function(data) {
            dfd.resolve(data);        //改变运行状态为“已完成”,立即触发done() 
        }      
     });
     return dfd.promise();  
}

$.when(sJson()).then(function(status){
      //如果then()只有一个参数，等同于done
      //成功--失败--通知
})

dfd.resolve();   //“已完成”
dfd.reject();     //“已失败”
dfd.notify();      //“通知(多次)”
{% endhighlight %}


下面的代码是我所碰到问题然后的解决办法，如果你还想了解更多的`deferred`的知识
请查看阮一峰写的[jQuery的deferred对象详解](http://www.ruanyifeng.com/blog/2011/08/a_detailed_explanation_of_jquery_deferred_object.html)



 





    