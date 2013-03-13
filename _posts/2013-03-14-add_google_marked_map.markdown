---
layout: post
title: 如何在网站中添加有城市标记的Google地图
category: Google
---

好多网站都会有这样的需求，展示一个地图，上面标记出一些地名或者城市。如下图所示。

![map_id](/images/map.png)

众所周知，Google和baidu都提供了地图服务，象上述这个小功能肯定提供了API来实现。本人没有开发过GIS，上网搜索后，找到了一个解决办法，纪录之，已供学习用。[参考](https://developers.google.com/maps/articles/v2tov3?hl=en)


+ 首先在Html的<head>标记中添加如下语句


`<script src="//maps.googleapis.com/maps/api/js?sensor=false&key=Your_API_Key" type="text/javascript"></script>`

+ 然后添加初始化地图的js函数initialize()

      var map = new google.maps.Map(
        document.getElementById('map_canvas'), {
          center: new google.maps.LatLng(39.943096343663754,116.4474801854858),
          zoom: 11,
          mapTypeId: google.maps.MapTypeId.ROADMAP
      });

      var marker = new google.maps.Marker({
            position: new google.maps.LatLng(39.943096343663754,116.4474801854858),
            map: map
      });

      var marker1 = new google.maps.Marker({
            position: new google.maps.LatLng(39.99855,116.470013),
            map: map
      });

	`google.maps.event.addDomListener(window, 'load', initialize);`


+ 接下来，在页面中添加map的div，代码如下

`<div id="map_canvas"></div>`

这样就可以在网页中看到有标志的Google地图了。


那么如何得到某个城市或者地方的准确经纬度呢？可以访问这个网址，输入地名，就可以得到对应的经纬度。


[http://www.gpsspg.com/maps.htm](http://www.gpsspg.com/maps.htm)