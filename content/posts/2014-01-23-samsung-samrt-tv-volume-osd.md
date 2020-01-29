---
layout: post
title: 'Samsung Samrt TV - volume OSD'
date: 2014-01-23
comments: true
categories: [Samsung]
---
## Samsung Samrt TV - volume OSD

假如要做影片類的 App, 音量控制算是重要的一環
建議維持 Samsung Samrt TV 預設的 OSD(On Screen Display), 假如自己刻 UI, 會有許多要顧及的地方, 會較費時

### How to add code to show volume OSD

* HTML

```html
<!-- for volume SOD -->
<object id="pluginObjectNNavi" border="0" classid="clsid:SAMSUNG-INFOLINK-NNAVI" style="opacity:0.0;background-color:#000000;width:0px;height:0px;"></object>
<object id="pluginObjectTVMW" border="0" classid="clsid:SAMSUNG-INFOLINK-TVMW"  style="opacity:0.0;background-color:#000000;width:0px;height:0px;"></object>

<!-- add plugin js -->
<script type='text/javascript' language='javascript' src='$MANAGER_WIDGET/Common/API/Plugin.js'></script>
```

* JavaScript

```javascript
// add pluginAPI
var pluginAPI = new Common.API.Plugin();

// set volume OSD(On Screen Display)
window.onShow = Main.volumeOSD;

Main.volumeOSD=function()
{
	var NNaviPlugin = document.getElementById("pluginObjectNNavi");
	pluginAPI.SetBannerState(1);
	NNaviPlugin.SetBannerState(2);
	pluginAPI.unregistKey(tvKey.KEY_VOL_UP);
	pluginAPI.unregistKey(tvKey.KEY_VOL_DOWN);
	pluginAPI.unregistKey(tvKey.KEY_MUTE);
	pluginAPI.unregistKey(262);
	pluginAPI.unregistKey(147);
	pluginAPI.unregistKey(45);
	pluginAPI.unregistKey(261);
}
```

### Example

[Samsung example zip](https://app.box.com/s/8xclf7olt14p2uvqxepm)

* HTML

```html
<!DOCTYPE html>
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<title>Samsung_miiiTV</title>

		<!-- TODO : Style sheets code -->
		<link rel="stylesheet" href="app/stylesheets/Main.css" type="text/css">

		<!-- TODO: Plugins -->

	</head>

	<body onload="Main.onLoad();" onunload="Main.onUnload();">

		<!-- Dummy anchor as focus for key events -->
		<a href="javascript:void(0);" id="anchor" onkeydown="Main.keyDown();"></a>

		<!-- for volume SOD -->
		<object id="pluginObjectNNavi" border="0" classid="clsid:SAMSUNG-INFOLINK-NNAVI" style="opacity:0.0;background-color:#000000;width:0px;height:0px;"></object>
		<object id="pluginObjectTVMW" border="0" classid="clsid:SAMSUNG-INFOLINK-TVMW"  style="opacity:0.0;background-color:#000000;width:0px;height:0px;"></object>

		<!-- TODO: your code here -->
	</body>
	<!-- TODO : Common API -->
	<script type='text/javascript' language='javascript' src='$MANAGER_WIDGET/Common/API/Plugin.js'></script>
	<script type="text/javascript" language="javascript" src="$MANAGER_WIDGET/Common/API/Widget.js"></script>
	<script type="text/javascript" language="javascript" src="$MANAGER_WIDGET/Common/API/TVKeyValue.js"></script>

	<!-- TODO : Javascript code -->
	<script language="javascript" type="text/javascript" src="app/javascript/Main.js"></script>
</html>

```

* JavaScript

```javascript
var widgetAPI = new Common.API.Widget();
var tvKey = new Common.API.TVKeyValue();
// add pluginAPI
var pluginAPI = new Common.API.Plugin();

var Main =
{

};

Main.onLoad = function()
{
	// Enable key event processing
	this.enableKeys();
	widgetAPI.sendReadyEvent();
	// set volume OSD(On Screen Display)
	window.onShow = Main.volumeOSD;

};

Main.volumeOSD=function()
{
	var NNaviPlugin = document.getElementById("pluginObjectNNavi");
	pluginAPI.SetBannerState(1);
	NNaviPlugin.SetBannerState(2);
	pluginAPI.unregistKey(tvKey.KEY_VOL_UP);
	pluginAPI.unregistKey(tvKey.KEY_VOL_DOWN);
	pluginAPI.unregistKey(tvKey.KEY_MUTE);
	pluginAPI.unregistKey(262);
	pluginAPI.unregistKey(147);
	pluginAPI.unregistKey(45);
	pluginAPI.unregistKey(261);
}

Main.onUnload = function()
{

};

Main.enableKeys = function()
{
	document.getElementById("anchor").focus();
};

Main.keyDown = function()
{
	var keyCode = event.keyCode;
	alert("Key pressed: " + keyCode);

	switch(keyCode)
	{
		case tvKey.KEY_RETURN:
		case tvKey.KEY_PANEL_RETURN:
			alert("RETURN");
			widgetAPI.sendReturnEvent();
			break;
		case tvKey.KEY_LEFT:
			alert("LEFT");
			break;
		case tvKey.KEY_RIGHT:
			alert("RIGHT");
			break;
		case tvKey.KEY_UP:
			alert("UP");
			break;
		case tvKey.KEY_DOWN:
			alert("DOWN");
			break;
		case tvKey.KEY_ENTER:
		case tvKey.KEY_PANEL_ENTER:
			alert("ENTER");
			break;
		default:
			alert("Unhandled key");
			break;
	}
};

```
