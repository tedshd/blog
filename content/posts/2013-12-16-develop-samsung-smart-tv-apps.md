---
layout: post
title: 'Develop Samsung Smart TV Apps'
date: 2013-12-16
comments: true
categories: [Samsung]
---
## Develop Samsung Smart TV Apps

由於最近應公司需求而開始要開發 Samsung 的 Smart TV 上的 App
身為一個前端攻城獅要去開發電視的 App?
沒想到 Smart TV 的 App 竟然是用前端技術寫的(HTML, JavaScript, CSS)
Smart TV 是 base on Linux
所以效能似乎 OK?
於是就來研究一下
[SAMSUNG SMART TV APPS Developer Forum](http://www.samsungdforum.com/)
載 SDK 與 TV 模擬器(除非 money 多多直接買一台 Smart TV, 不過有開發過 Android 的都知道 **模擬器都是假的** )
[SDK Download(Software development kit)](http://www.samsungdforum.com/Devtools/SdkDownload)
載 virtualBox
[Oracle VM VirtualBox](https://www.virtualbox.org/)

### 建立開發環境

1. 裝 virtualBox
3. 開 SDK(用超吃資源的 eclipse Orz)
2. 開 virtualBox, 掛 Smart TV Emulator
  * 檔案 -> 匯入應用裝置(選擇下載的 Smart TV Emulator)
  * 設定值 -> 共用資料夾 -> 編輯(資料夾名稱 / Apps, 資料夾路徑 / /Users/tedshd/Documents/workspace (SDK workspace 路徑))

### 開始開發

懶得看下去有 YouTube 影片
[Samsung smart tv development tutorial - 01](https://www.youtube.com/watch?v=oujq32KKg4M)
[Samsung smart tv development tutorial - 02](https://www.youtube.com/watch?v=wgdewmQr7sM)
[Samsung smart tv development tutorial - 03](https://www.youtube.com/watch?v=C8WlV9FqoFU)
[GTUG 的 Samsung Smart TV開發簡介](https://www.youtube.com/watch?v=u5DvRiAfD7Q)
圖文版

1.建立 JavaScript 專案

![全熒幕_2013_12_16_下午5_14.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/xQzOznimQe2pKD77pl0A_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_14.png)

![全熒幕_2013_12_16_下午5_15.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/Dd7yUTOOSCCwkpAsSl22_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_15.png)

![全熒幕_2013_12_16_下午5_16.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/du6udFsTS3OQCcOGg3ac_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_16.png)

![全熒幕_2013_12_16_下午5_17.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/JZtas4eeQL6fSqt32YU6_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_17.png)

![全熒幕_2013_12_16_下午5_18.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/gGKbDf5sQIu7f0hZRqQQ_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_18.png)

![全熒幕_2013_12_16_下午5_19.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/9PRttEwfQ4e0c0I9JC6T_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_19.png)


2.開始修改

![全熒幕_2013_12_16_下午5_21.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/bvpgZL3QPyc6HRePxK4V_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_21.png)

![全熒幕_2013_12_16_下午5_23.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/FYXcgt1QTYuxBnz5lfJx_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_23.png)


3.Run 模擬器

![全熒幕_2013_12_16_下午5_28.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/vPhbXInRai7FvFISrvHI_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_28.png)

![全熒幕_2013_12_16_下午5_36.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/is1SR6DMT6lNhNdDvpnw_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_36.png)

![全熒幕_2013_12_16_下午5_37.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/2rXHSi6TdKkNPMMD1OhD_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_37.png)

![全熒幕_2013_12_16_下午5_38.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/c8cZqxUGSpGRVy4C3el5_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_38.png)

![全熒幕_2013_12_16_下午5_40.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/1zsXeDWgQkefq3VyPkz8_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_40.png)

![全熒幕_2013_12_16_下午5_41.png](http://user-image.logdown.io/user/3170/blog/3202/post/166874/jOXKDQa5RV4u1iwdG2sw_%E5%85%A8%E7%86%92%E5%B9%95_2013_12_16_%E4%B8%8B%E5%8D%885_41.png)



### Test app on TV

先決條件
開發的 PC or Mac 必須有 server
因為它是把 app 打包後由 smart TV 連 server 去抓 app
**在 smart TV 上 Samung 帳號要用 develop 才能跑出抓 app 的選項**
基本上照著底下 Testing Your Application on TV 做就可以順利把 app 丟到 TV 上
[Debugging and Testing Applications](https://www.samsungdforum.com/Guide/art00012/index.html)
[Testing Your Application on a TV](https://www.samsungdforum.com/Guide/art00013/index.html)
[Testing Your Application on a TV for 2014](http://www.samsungdforum.com/Guide/art00121/index.html)

### Some Tip

在打包 app 時 config.xml

```xml
<ver itemtype="string">0.100</ver>
```

版號必須與打包時的版號相同

SDK 的大版號對應該年度的 Samsung Smart TV

* SDK Emulator 1.5 - for 2010 platform
* SDK Emulator 2.5 - for 2011 platform
* SDK Emulator 3.5 - for 2012 platform
* SDK Emulator 4.5 - for 2013 platform
* SDK Emulator 5.0 Beta - for 2014 platform

所以要用其他年度的 TV 上必須要用對應的 SDK 打包
其中也必須小心 API 的支援程度
目前發現新版 SDK(5.0) 打包可在 2013 年的 TV 跑

在 app 中需有提示 user 遙控器哪些按鍵有功能的 info bar

在 app 最上層(或是所謂的首頁)按返回須有 confirm 的行為

影片相關的 app 需注意音量控制

在 web 跑爽爽, 到 TV 上可不一定
有可能有 JavaScript method、event or API 不支援
也有網路連線上速度的問題, 拉 API 時會卡住

網路中斷 Samsung Smart TV 會出 notification, 所以可不處理, 但有時不靈光

在 eclipse 接 TV 的 log
[Refer - How to view logs in Samsung Smart TV log viewer](http://stackoverflow.com/questions/15922620/how-to-view-logs-in-samsung-smart-tv-log-viewer)

### Some Documents

[Introduction to Smart TV platform](https://www.samsungdforum.com/Guide/c02/index.html)
[JavaScript](https://www.samsungdforum.com/Guide/art00015/index.html)
[UI](https://www.samsungdforum.com/Guide/art00023/index.html)
[Device API](https://www.samsungdforum.com/Guide/ref00011/index.html)
[Web Device API](https://www.samsungdforum.com/Guide/ref00008/index.html)
[Player Specification](https://www.samsungdforum.com/Guide/rel00010/index.html) video/audio support
[CSS3 Browser Specification](https://www.samsungdforum.com/Guide/art00065/index.html)
[The difference between Return and Exit keys](http://www.samsungdforum.com/Guide/tec00101/index.html)
[TVKeyValue Object](http://samsungdforum.com/Guide/ref00006/common_module_tvkeyvalue_object.html) remote control key code

### Issue

* deploy apps on TV version and update not easy
* deploy apps have cache?
* Samsung some sample code can't run on TV
* device API, web device API 支援不多
* third party login(Fb, Google ...)[Single Sign-On](https://www.samsungdforum.com/Guide/art00077/index.html) / [Using Single Sign-On (SSO)](https://www.samsungdforum.com/Guide/tut00053/index.html)
