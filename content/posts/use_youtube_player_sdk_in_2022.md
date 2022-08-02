---
title: "2022 年使用 YouTube player sdk"
date: 2022-08-02T13:04:37+08:00
draft: false
categories: [JavaScript, YouTube]
---

## 前言

距離上次使用 YouTube Player API 已經是 2014 年的事了

不知不覺也過了超久了

剛好最近公司有相關的需求需要在 App 中能夠播放 YouTube 的影片

原本想說 App 應該和我沒關係了

所以這次準備躺平(誤

結果還是被牽扯進來了...

## 2022 年當前如何使用 YouTube player SDK

沒想到不看還好, 一看就準備 GG

一開始把文件丟給 Android 和 iOS

Android 那邊說無法用

我當下????

文件都寫得好好的, 為何說無法用

和 Android 一起討論了一下, 才確認了一件事

原來 Android 為了統一 libary, 在 2018 年開始推行 Androidx 要取代 android.support

最大的改變是 namespace 的變動, 雖然官方有[工具](https://developer.android.com/studio/command-line/jetifier)可以對第三方 lib 做轉換, 但也會是一個大換血, 而且對比較老舊的套件還會需要處理 activity 和 fragment 的處理, 因為現今大多的 Android 都以 fragment 實作 UI 了

所以 Android 開發表示兩手一攤

所以只能接下來用 iframe player 處理了

之後我這邊又再次和 iOS 確認了一下

因為依照[文件](https://developers.google.com/youtube/v3/guides/ios_youtube_helper#best-practices-and-limitations)說明 iOS 的 player 底層還是用 webview 封裝起來的, 所以應該沒問題才對

然後 iOS 很高興的表示, 既然 Android 都要用 webview 搞了, 那 iOS 也一起用吧

真的是很感謝 client 端幫我創造工作機會...

## 到了 2022 API 發生了許多變動

因為當年的 prototype code 還留著, 所以秒完成

但還是要看一下文件看看有什麼變動

一看下去才發現真的變動一卡車東西

也讚嘆 Google 真的是很認真在維護與更新文件

都有變動紀錄

[參數部分可以看這裡](https://developers.google.com/youtube/player_parameters#Revision_History)

[播放器的 API 變動可以看這裡](https://developers.google.com/youtube/iframe_api_reference#Revision_History)

主要是這幾年也因為在瀏覽器上因應對 video 的支援做蠻多播放邏輯的變動

部分是因為 YouTube 的服務策略做變動

以前 YouTube player 可以魔改到 YouTube 自己都認不出來(可以關掉超多顯示資訊, 完全客製化控制項)

現在已經無法了...

像是左上的影片標題, 右上的選單功能, 右下的 YouTube logo 現在都無法隱藏了...

還好現在播放一段時間後會自動隱藏這些資訊

## 串接 webview 特有的問題

有些問題是在 webview 上特有的問題

幾乎都是 Android 的問題

就 Android 的問題最多 XD

這裡記錄一下

1. 處理自動播放的問題

礙於瀏覽器政策, 得是靜音才能自動播放, 或是要有使用者互動才能自動播放

我們採用的方式, 是靜音自動播放, 也避免使用者一開始被影片聲音嚇到

2. Android 的播放器會因為滑動行為被判定長壓啟動選單

因為會是個 feed 列表呈現影片, 滑動到畫面內就會播放畫面中的影片

所以有遇到個問題是頁面在滑動時手指停留在播放器中會誤判長壓造成啟動播放器選單

解決方式還是老樣子在 webview 的 player 上面蓋一層透明遮罩, 自己客製控制 UI

3. 在 Android 當影片在播放時使用 Youtube SDK API 取消靜音會有無法播放影片問題

這問題追了一下, 確認和 iframe player api 還有 JS 無關後, 就換個思路想會不會是 webview 有啥限制(因為在 browser 都正常)

下了幾個關鍵字丟給 Google 後查到 webview 有個 `setMediaPlaybackRequiresUserGesture` 的設定

```Java
webView.getSettings().setMediaPlaybackRequiresUserGesture(false)
```

設定成 false 的意思是在 webview 不用有任何互動就可以自動播放

想說會不會有關聯, 所以請 Android 開發那邊設定

結果就解決這問題了

[Refer - Auto play video in webview](https://stackoverflow.com/questions/38975229/auto-play-video-in-webview)

4. 全螢幕的功能

iOS 的全螢幕會給系統的播放器

Android 的全螢幕功能會受限於 webview 的大小

所以這部分的差別也得注意