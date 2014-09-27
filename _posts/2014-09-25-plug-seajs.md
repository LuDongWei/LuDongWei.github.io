---
layout: blog
title: seajs的简单运用
categories: [plug]
logo: plug.png 
tags: [plug,seajs]
---

[seajs](http://seajs.org/docs/)的使用感觉对我来说真的很棒。就像它的官网说的那样

-  **简单友好的模块定义规范:**Sea.js 遵循 CMD 规范，可以像 Node.js 一般书写模块代码。
-  **自然直观的代码组织方式:**依赖的自动加载、配置的简洁清晰，可以让我们更多地享受编码的乐趣。

如果你想了解更多可以去它的[官网](http://seajs.org/docs/)查看，上面还有搭建它的整个流程。如果要学习它的话按照上面的流程做一遍，就可以使用它了。
下面我把自己整理的常用写法罗列下（待补充）。

##seajs简单配置
{% highlight  javascript %}
//config.js
seajs.config({
      base:"../sea-modules/",
      alias:{
         "jquery":"...."
      } 
})
{% endhighlight %}

>`base`：默认模块相对`sea.js`的路径来解析，设置后相对于`base`的路径来解析
>
>`alias`: 简化模块的标识，方便项目的迁移


##seajs模块的写法
{% highlight  javascript %}
//seckilling.js 
define(function (require,exports,module){
       var $=require("jquery");   //引入依赖
       
       var seckill=exports;          //对外接口

       var defaults={
             name:"",
             onEnd:function(a,b){
             }
       }
       
       var SSSSSS;                    //大写为接口
       var callback;
       var data=[];
       
       seckill.init=function(options,callback_){
             var opts = $.extend(defaults, options || {});   //合并信息
             SSSSSS= 'http://m.mbaobao...' + defaults.seckill_id + '.html';

             data.push(opts)
             console.log(data)   
             //!! 输出，2次输出相同的结果。但是如果打断点的话输出结果会不相同
               原因 console.log 不能...
 
                                                              
             opts.onEnd("a","b");   //输出 
                      
             callback=callback_;
       }

      seckill.start=function(){
            console.log(data)                   //!!
      }
                
})
{% endhighlight %}

>`var opts = $.extend(defaults, options || {});`       //合并信息 改变defaults
>
>`var opts = $.extend({}，defaults, options || {});`   //合并信息 不改变defaults

##seajs常见使用
{% highlight  javascript %}
seajs.use("./seckilling",function(SK){
        SK.init(
             name:"aa",
             onEnd:function(a){
                 alert(a);
             }
         );
        SK.init(name:"bb");
        
        SK.start();     // ["aa","bb"]
})
{% endhighlight %}


##预加载
{% highlight  javascript %}
require.async('jquery-plugin/simplemodal/1.4.4/simplemodal', function(simplemodal){
           simplemodal($);  //加载不影响主页面程序
})
{% endhighlight %}    