---
layout: post
title: IE特殊处理三则
category: IE
---


做过前台开发的人员，或多或少都会碰到IE的兼容问题。

最近在给[琥珀网](http://www.hupo.tv)做首页的时候，也碰到了IE显示问题。主要有三个问题：

+ 节目表单无法正确显示
+ IE7下，首页的jwplayer位置不正确
+ 首页中，各频道图片之间的间距显示不正确

有问题不可怕，可怕的是找不到问题所在，以及没有跟踪的办法。

---

琥珀网中的节目表单使用一个叫[CHAP Links Library](http://almende.github.com/chap-links-library/)的timeline插件实现json数据动态加载。这个功能在FF，Chrome，Safari中都能正确工作，只有在IE中，无法显示节目单。

起初我一点头绪都没有，只要在js代码中增加alert语句来调试，唯一得到的就是代码可以正确的执行，就是结果不显示。

只好在IE的开发人员工具F12的帮助下，给js代码设置断点，搜索问题。

在timeline.js的draw方法中'this.setData(data)'设置一个断点，查看一下data数据，果然在这里发现问题，data数据中所有的日期字段都是"Undefined"。回到Chrome中查询对应的数据，发现这些日期都没有问题。


    links.Timeline.prototype.draw = function(data, options) {
      this.setOptions(options);

       // read the data
       this.setData(data);

       // set timer range. this will also redraw the timeline
       if (options && (options.start || options.end)) {
           this.setVisibleChartRange(options.start, options.end);
       }
       else if (this.firstDraw) {
           this.setVisibleChartRangeAuto();
       }

       this.firstDraw = false;
    };

这些日期数据都是ruby传给js的，形式如，str = 'Wed Mar 20 16:05:05 +0800 2013'，然后把这个字符串传递给js的Date函数。

    var time = new Date(str);  
    // str ='Wed Mar 20 16:05:05 +0800 2013'

上面的这句话在Chrome，FF，Safari中都能正确的生成JS下的日期，只有IE下无法实现。为了搞清楚，特意google一下JS中Date的构造函数，[参见](http://www.w3schools.com/jsref/jsref_obj_date.asp)

原来JS中，Date对象的定义有如下几种形式：

    var d = new Date();

    var d = new Date(milliseconds);

    var d = new Date(dateString);

    var d = new Date(year, month, day, hours, minutes, seconds, milliseconds);


其中dateString,只支持如下几种形式，当然不局限于如下形式：

    October 13,1975 11:13:00

    October 13,1975 11:13

    October 13,1975

    2010-06-09 15:20:00

    2010-06-09 15:20

    2010-06-09

    2010-06

    2010


对于IE来说，上面的'Wed Mar 20 16:05:05 +0800 2013'这种形式是不支持的，所以改为Date(milliseconds)，问题就迎刃而解。

---

关于jwplayer位置不正确的问题，首先了解，jwplayer.setup("div_id")的方法，会生成如下代码：

原代码
    <div id="div_id">jwplayer</div>

新代码
    <div id='div_id_wrapper'><object id='div_id'>...</object></div>

所以在写css的时候，可以通过设置div_id_wrapper这个div样式来实现想要的效果。

本例中，还涉及到position:relative在IE7下不工作的问题。具体解决方案，[参见](http://snook.ca/archives/html_and_css/position_relative_overflow_ie/)，解释的很清楚。

---

关于第三个问题，没有修改任何css代码，只是在网页的头部添加了<!DOCTYPE> transitional DTD。

    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

具体[参见](http://www.w3school.com.cn/tags/tag_doctype.asp)


