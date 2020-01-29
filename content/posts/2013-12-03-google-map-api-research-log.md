---
layout: post
title: 'Google map api - research log'
date: 2013-12-03
comments: true
categories: [javascript, google]
---
## Google map api - research log

### Introduction

使用 [Google Maps JavaScript v3](https://developers.google.com/maps/documentation/javascript/?hl=zh-tw)
[static map](https://developers.google.com/maps/documentation/staticmaps/?hl=zh-tw) 嵌入地圖到網頁中以圖片方式呈現
[使用限制](https://developers.google.com/maps/documentation/javascript/usage?hl=zh-tw) 基本上不要一日載超過 25000 次都沒事
[區域化 - 語系](https://developers.google.com/maps/documentation/javascript/basics?hl=zh-tw#Localization)

[Library](https://code.google.com/p/google-maps-utility-library-v3/wiki/Libraries)


### Init map

```html
<!DOCTYPE html>
<!--使用 <!DOCTYPE html> 宣告，將應用程式宣告為 HTML5-->
<html>
<head>
<meta charset="utf-8">
<title>Google_map_api_basic</title>
<meta name="viewport" content="initial-scale=1.0, user-scalable=no" />
<!--最新的瀏覽器會將使用此 DOCTYPE 宣告的內容以「標準模式」呈現，也就是說，您的應用程式應更具備跨瀏覽器相容性。此外，DOCTYPE 也設計成會逐漸適應，但無法理解它的瀏覽器將會忽略它，而採用「快速模式」顯示內容。請注意，有些 CSS 在快速模式中可以運作，但在標準模式中卻無效。具體來說，所有百分比的大小都必須繼承父區塊項目，但這些上階中如有任何一個無法指定大小，就會假設為 0 x 0 像素大小。基於這個理由，我們加入了下列 <style> 宣告-->
<style type="text/css">
html {
    height: 100%;
}
body {
    height: 100%;
    margin: 0px;
    padding: 0px;
}
#map_canvas {
    height: 100%;
}
</style>
<!--這個 CSS 宣告表示地圖容器 <div> (名為 map_canvas) 應使用 HTML 主體的 100% 高度。請注意，我們也必須特別宣告 <body> 和 <html> 的這些百分比-->
<script type="text/javascript" src="https://maps.google.com/maps/api/js?sensor=true"></script>
<!--使用 script 標記來涵蓋 Maps API JavaScript-->
<!--請注意，我們也必須設定 sensor 參數，以指出這個應用程式是否有使用感應器來判斷使用者的位置。必須明確地將這個值設為 true 或 false-->
</head>
<body onload="initialize()">
<!--從 body 標記的 onload 事件初始化地圖物件-->
  <div id="map_canvas" style="width:100%; height:100%"></div>
  <!--建立 div 元素 (名稱為「map_canvas」) 來容納「地圖」-->
</body>
<!--建立 JavaScript 物件實字以存放多個地圖屬性-->
<!--JavaScript 函式以建立「地圖」物件-->
<script type="text/javascript">
function initialize() {
    var myOptions = {
        center: new google.maps.LatLng(25.05060, 121.51870),
        zoom: 8,
        mapTypeId: google.maps.MapTypeId.ROADMAP
    };
    var map = new google.maps.Map(
        document.getElementById("map_canvas"),
        myOptions
    );
}

</script>
</html>
```

### JavaScript map object

先建立地圖的設定
[地圖選項](https://developers.google.com/maps/documentation/javascript/tutorial?hl=zh-tw#MapOptions)

```javascript
var myOptions = {
    center: new google.maps.LatLng(25.05060, 121.51870),
    zoom: 8,
    mapTypeId: google.maps.MapTypeId.ROADMAP
};
```

* center 表示一開始地圖的中心位置
* zoom 地圖縮放(0 ~ 18)
* mapTypeId 地圖類型
  * ROADMAP 顯示 Google 地圖的正常、預設 2D 地圖方塊。
  * SATELLITE 可顯示攝影地圖方塊。
  * HYBRID 可顯示混合攝影地圖方塊與重要地圖項 (道路、城市名稱) 的地圖方塊圖層。
  * TERRAIN 可顯示實際起伏的地圖方塊，以呈現海拔高度和水域圖徵 (山嶽、河流等)。

初始化地圖
[地圖物件](https://developers.google.com/maps/documentation/javascript/tutorial?hl=zh-tw#google.maps.Map)

```javascript
var map = new google.maps.Map(
    document.getElementById("map_canvas"),
    myOptions
);
```

### Mark Google map

[標記](https://developers.google.com/maps/documentation/javascript/overlays?hl=zh-tw#Markers)
標記在地圖上的位置

```javascript
// list marks
var arr = new Array(
    {
        position: new google.maps.LatLng(25.05060, 121.51870),
        title: 'Hello World!'
    },
    {
        position: new google.maps.LatLng(25.056304, 121.522079),
        title: '春漾咖啡'
    }
);

// put marks in map
for (var i = 0; arr.length-1 >= i; i++) {
    var marker = new google.maps.Marker(arr[i]);
    marker.setMap(map);
};
```

### Info windows

[infowindows](https://developers.google.com/maps/documentation/javascript/infowindows)

標記上的 pop tooltip

```javascript
var infowindow = new google.maps.InfoWindow();
```

#### Method

* setContent()
* open()
* close()

#### [Properties](https://developers.google.com/maps/documentation/javascript/reference#InfoWindowOptions)

* content
* disableAutoPan
* maxWidth
* pixelOffset
* position
* zIndex

### Event

[事件](https://developers.google.com/maps/documentation/javascript/events?hl=zh-tw)
Google map api 提供許多與 map 有關的事件

### Style

[樣式標記地圖](https://developers.google.com/maps/documentation/javascript/styling?hl=zh-tw)
