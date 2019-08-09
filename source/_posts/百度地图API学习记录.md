---
title: 百度地图API学习记录
date: 2018-08-27 10:58:25
tags: 记录
categories: 编程
---

### 百度地图的API

#### 创建地图

var map = new BMap.Map("container")  "container"是html中标签的id名

```js
var map = new BMap.Map("container");          // 创建地图实例  
var point = new BMap.Point(116.404, 39.915);  // 创建点坐标  
map.centerAndZoom(point, 15);                 // 初始化地图，设置中心点坐标和地图级别 
```

#### 地图控件

添加控件

```js
map.addControl(new BMap.NavigationControl());
```

添加多个地图控件

```js
map.addControl(new BMap.NavigationControl());    
map.addControl(new BMap.ScaleControl());    
map.addControl(new BMap.OverviewMapControl());    
map.addControl(new BMap.MapTypeControl());    
map.setCurrentCity("北京"); // 仅当设置城市信息时，MapTypeControl的切换功能才能可用  
```

#### 地图标注

```js
var marker = new BMap.Marker(new BMap.Point(116.404, 39.915)); //点
var polyline = new BMap.Polyline([
    new BMap.Point(114.399, 39.910),
	new BMap.Point(116.405, 39.920),
	new BMap.Point(116.425, 39.900)
], {strokeColor:"blue", strokeWeight:2, strokeOpacity:0.5}); //创建折线
	var circle = new BMap.Circle(point,500,{strokeColor:"blue", strokeWeight:2, strokeOpacity:0.5}); //创建圆
	
	var polygon = new BMap.Polygon([
		new BMap.Point(116.387112,39.920977),
		new BMap.Point(116.385243,39.913063),
		new BMap.Point(116.394226,39.917988),
		new BMap.Point(116.401772,39.921364),
		new BMap.Point(116.41248,39.927893)
	], {strokeColor:"blue", strokeWeight:2, strokeOpacity:0.5});  //创建多边形
	
	var pStart = new BMap.Point(116.392214,39.918985);
	var pEnd = new BMap.Point(116.41478,39.911901);
	var rectangle = new BMap.Polygon([
		new BMap.Point(pStart.lng,pStart.lat),
		new BMap.Point(pEnd.lng,pStart.lat),
		new BMap.Point(pEnd.lng,pEnd.lat),
		new BMap.Point(pStart.lng,pEnd.lat)
	], {strokeColor:"blue", strokeWeight:2, strokeOpacity:0.5});  //创建矩形
	
	//添加覆盖物
	function add_overlay(){
		map.addOverlay(marker);            //增加点
		map.addOverlay(polyline);          //增加折线
		map.addOverlay(circle);            //增加圆
		map.addOverlay(polygon);           //增加多边形
		map.addOverlay(rectangle);         //增加矩形
	}
	//清除覆盖物
	function remove_overlay(){
		map.clearOverlays();         
	}
```

获取地图marker的位置

```js
var marker = new BMap.Marker(point); // 创建标注
var p = marker.getPosition();  //获取marker的位置
p.lng // 经度
p.lat // 纬度

```

从多个点里删除特定点

- 通过marker的label删除特定点

```js
var marker = new BMap.Marker(point); // 创建标注
var label = new BMap.Label("事故地点")；
map.addOverlay(marker);
marker.setLabel(label);

function deletPoint() {
    var allOverlay = map.getOverlays();
    for (var i = 0; i < allOverlay.length-1; i++) {
        if(allOverlay[i].getLabel().content == "事故地点") {
            map.removeOverlay(allOverlay[i]);
            return false;
        }
    }
} // 只删除内容为"事故地点"的marker
```

