---
layout: post
title: 'Windows 8.1 app develop - Introduction'
date: 2014-06-23
comments: true
categories: [windows, javascript]
---
## Windows 8.1 app - Introduction

Develop Win 8.1 app with JavaScript.

1. 死心吧, 請準備一台 Windows 8.1 的電腦(一直以來我都以為生為前端攻城獅只要用 Mac 就可以打天下了)

2. 下載 [Visual Studio 2013](http://www.visualstudio.com/zh-tw/downloads), 要下載 Visual Studio Express 的版本

3. 開始努力地讀文件 ~~[Doc](http://msdn.microsoft.com/en-us/library/windows/apps/br211385.aspx)~~

### <strong style="color:red">Notice & Tip</strong>

先了解一些限制與規範以免踩雷

* Microsoft 提供 [WinJS](https://github.com/winjs/winjs) 來協助開發 Windows 8.1 app

* 無法使用網路的 source
	* 無法使用 remote 的 CSS or JavaScript, 必須全部 download 下來

* 無法直接使用 iframe
	* `package.appxmainifest` -> `內容 URI`, 把 iframe url 設成例外, 但是該 url 必須用 https
  * 使用 `x-ms-webview` tag 來代替 `iframe`, [x-ms-webview element | x-ms-webview object](http://msdn.microsoft.com/en-us/library/windows/apps/dn301831.aspx)


#### Handle AJAX

在開發 Windows 8.1 時, 並不能直接的 `XMLHttpRequest` 處理 AJAX 行為, 需用 WinJS 來處理
[WinJS.xhr function](http://msdn.microsoft.com/en-us/library/windows/apps/xaml/br229787.aspx)


[Refer - Windows8軟體開發小學堂(十)：使用WinJS自訂Javascript類](https://software.intel.com/sites/landingpage/tw/windows8-college-10.php)
[Refer - Windows8軟體開發小學堂(十一)：使用WinJS自訂Javascript的名字空間](https://software.intel.com/sites/landingpage/tw/windows8-college-11.php)
[Refer - Windows8軟體開發小學堂(十二)：使用WinJS在已有Namespace中添加新成員](https://software.intel.com/sites/landingpage/tw/windows8-college-12.php)
[Refer - Windows8軟體開發小學堂(十三)：給Metro應用添加Wide Logo](https://software.intel.com/sites/landingpage/tw/windows8-college-13.php)
[Refer - Windows8軟體開發小學堂(十四) : 修改Metro應用的Splash Screen](https://software.intel.com/sites/landingpage/tw/windows8-metro-splash-screen.php)
