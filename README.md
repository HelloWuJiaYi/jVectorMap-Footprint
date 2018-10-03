# 教你用 jVectorMap 制作属于自己的旅行足迹

![我的足迹地图](http://wx1.sinaimg.cn/large/cf5b72a1ly1fvv1gupvz0j20xx0op760.jpg)

## jVectorMap

JVectorMap 是一个优秀的、兼容性强的 jQuery 地图插件。

它可以工作在包括 IE6 在内的各款浏览器中，矢量图输出，除官方提供各国地图数据外，用户可以使用数据转换程序定制地图数据。例如街道地图、小区地图等等。

JVectorMap 官方网站提供了很多相关文档和使用示例，感兴趣的小伙伴可以自己研究一下。

官方网站：<http://jvectormap.com/>

![jVectorMap](http://wx4.sinaimg.cn/large/cf5b72a1ly1fvv2t7olhjj20ss0e8jvo.jpg)

今天教大家通过 jVectorMap 制作旅行足迹地图，最终的效果可以查看下面的 Demo 演示（中国），并教大家如何将制作好的足迹地图嵌入到我们自己的博客中。

Demo : <http://download.wujiayi.vip/map/index.html>

## 目录结构

![](http://wx1.sinaimg.cn/large/cf5b72a1ly1fvv432zeqzj20b806gaaa.jpg)

- 红色框中的文件是必须要引入的内容。

- 绿色框中的文件是展示的地图，可自行到官网下载需要的地图 : <http://jvectormap.com/maps/world/world/>，拷贝到 js 目录。

- index.html 中需要添加足迹位置和相关样式。

## 开始

 `index.html` 分为三部分介绍：
 
 - 如何更换不同国家地图。
 
 
 - 如何修改地图颜色等相关样式。
 
 
 - 如何添加足迹位置。
 
## 第一部分：如何更换不同国家地图。
 
```html
<html>
	<head>
		<!--引入jQuery框架-->
		<script type="text/javascript" src="js/jquery-1.9.1.min.js"></script>
		<!--引入jVectorMap库-->
		<script type="text/javascript" src="js/jquery-jvectormap-1.2.2.min.js"></script>
		<!--引入样式表-->
		<link href="js/jquery-jvectormap-1.2.2.css" rel="stylesheet" media="screen">


		<!--引入中国地图数据库-->
		<script type="text/javascript" src="js/jquery-jvectormap-cn-merc-en.js"></script>

		<!--引入美国地图数据库-->
		<!--script type="text/javascript" src="js/jquery-jvectormap-us-aea.js"></script-->
		<!--引入世界地图数据库-->
		<!--script type="text/javascript" src="js/jquery-jvectormap-world-mill.js"></script-->

	</head>
<body>
```
提前下载需要的国家地图，拷贝到 js 目录下。

在 `<head>` 标签里引入地图数据： `<script type="text/javascript" src="js/地图文件名"></script>`

**注意** ：同时只能有一个地图库，注意不要引入多个地图数据。可以选择注释掉其他的，方便更改。

## 第二部分：如何修改地图颜色等相关样式。


```html
	<!--background-color: 地图背景颜色-->
	<div id="map" style="background-color:#353535"> </div>
	<script>
		$('#map').vectorMap({

			// 此处更改地图
			map: 'cn_merc_en',   // 中国地图
			//map: 'us-aea',     // 美国地图
			//map: 'world-mill', // 世界地图


			backgroundColor: 'transparent',
			zoomMin: 0.9, // 鼠标缩放时的最小比例
			zoomMax: 2.4, // 鼠标缩放时的最大比例
			focusOn: {
				x: 0.55,
				y: 2,
				scale: 0.9
			},
			regionStyle: {
				initial: {
					fill: '#e5e5e5',   // 地图颜色
					"fill-opacity": 1, // 省份（州）是否隐藏，鼠标滑动时显示; 1：显示，2：隐藏。
					stroke: 'none',
					"stroke-width": 0,
					"stroke-opacity": 1
				},
				hover: {
					fill: '#ccc',  // 鼠标滑动至某省份的高亮颜色。
					"fill-opacity": 0.8
				},
				selected: {
					fill: 'yellow'
				},
				selectedHover: {}
			},
			markerStyle: {
		        initial: {
		            fill: '#fd8888', // 足迹位置的填充颜色
		            stroke: '#fff'   // 足迹位置的描边颜色
		        },
				hover: {
					fill: '#fd2020', // 鼠标滑动至足迹位置后的填充颜色
					stroke: '#fff',  // 鼠标滑动至足迹位置后的描边颜色
					"fill-opacity": 0.8
				},
		    },
		});
	</script>
</html>

```
参照代码注释修改颜色和相关样式。

**千万注意** ：在更改地图时 `map: '地图名称'`  ，地图名称是地图数据文件名的后半部分。

例如：

美国地图文件名：jquery-jvectormap-us-aea.js

那地图的名称是：us-aea

**但是要注意把 `-` (横杠)更改成 `_`（下划线）。 否则不会显示地图。**

## 第三部分：如何添加足迹位置。

```html
	markers: [ // 足迹位置

		// {latLng: [经度（保留两位小数）, 纬度（保留两位小数）], name: '城市名称'},
		// 推荐查询经纬度网站：http://www.gpsspg.com/maps.htm

		{latLng: [39.90, 116.41], name: '北京'},
		{latLng: [31.24, 121.50], name: '上海'},

		{latLng: [46.06, 122.06], name: '内蒙古 - 乌兰浩特'}
	]

```

推荐查询经纬度网站：http://www.gpsspg.com/maps.htm

语法：`{latLng: [经度（保留两位小数）, 纬度（保留两位小数）], name: '城市名称'},`。

## 如何嵌入式到博客中

```html
<iframe style="max-width: 100%" 
      frameborder="no" 
      border="0" 
      marginwidth="0" 
      marginheight="0" 
      width="100%" 
      height="750px" 
      src="替换成你的足迹地图链接">                                        
</iframe>

```
把制作好的足迹地图文件放在服务器上，把访问连接放在 `src` 中。

然后将上面的代码复制到你的博客页面上即可。

可适配手机端和等比例缩放。

## 获取源码

GitHub : <https://github.com/HelloWuJiaYi/jVectorMap-Footprint>

## 广告时间

欢迎访问我的个人博客:

<http://www.wujiayi.vip>

我的微信公众号：

`吴佳轶同学`



