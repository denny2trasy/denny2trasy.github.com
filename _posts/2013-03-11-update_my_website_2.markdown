---
layout: post
title: 我的建站经历(续)
category: TechExper
---

## 第四天 ##

**网站功能**

博客不用太复杂，能发文章，评论即可，文章可以按类别和时间归类就行。

Jekyll提供了基本的Post维护，虽然说有category，tag等标记功能，但是文章的归档就没有。幸好它提供plugin，自己能够实现想要的功能。


对于一篇Post文章，其中包含两类数据：

* YAML Front Matter标记：记录文章的属性，例如layout，title，category，以及任何自己想定义的属性，这些标记都会被Liquid templating engine解析，并且记录到data数据中，等到render这些页面的时候，用Liquid标记来获得这些数据，展示在新生成的页面中。[参考](https://github.com/mojombo/jekyll/wiki/template-data)

* Liquid标记：两种语法，一是显示数据，二是操作数据。[参考]( https://github.com/Shopify/liquid/wiki/Liquid-for-Designers)


有了如上的知识，可以发表自己的post，可是如果想让文章归类显示，在首页中弄个category list块，还是需要plugin的帮助。

起初想自己按照[说明]( https://github.com/mojombo/jekyll/wiki/Plugins)实现categary和archive的文章生成功能和categary_list列表块。可是不知道什么原因，generate总是不执行，无法生成页面，而且还找不到好的调试手段。
改变策略，直接把现成的plugin copy过来还是无法生成，最后翻看文档才明白，我在_config配置文件中，把safe设置为true，这样所有的_plugins都被屏蔽。

算是搞定一个问题，继续中…

## 第五天 ##

优化layout，使用include，layout可以嵌套，layout中大量使用Liquid标记。

## 第六天 ##

完善plugin，给网站添加[comment](http://www.disqus.com)功能。

## 第七天 ##

学习[markdown]( http://wowubuntu.com/markdown/)语法，部署代码

github page不支持unsafe plugin， 所以我自己写的plugin在page上无法执行，刚碰到这个问题时，让我很是疑惑，在本地一点问题都没有，怎么放上去就是没有效果，最后才找到，page的config文件中safe默认是打开的。
为了解决这个问题，github提供了两种方案，[参见]( https://help.github.com/articles/pages-don-t-build-unable-to-run-jekyll)，思来想去，我还是觉得采取第一种方案比较简单。

至此，我的博客重新搞定，坚持写下去是目前的首要任务，这个建站过程就是新开篇吧！
