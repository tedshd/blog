---
layout: post
title: 'Web Develop on mobile web & WebView'
date: 2018-09-16
comments: true
categories: [mobile]
---
## Web Develop on mobile web & WebView

因為某些原因必須把這些東西紀錄一下

其實實在太多東西要寫但實在是太忙且有點沒動力寫文章...

會分成兩個 mobile OS 與 mobile browser 加上 WebView 共 4 部分

* Android
  * mobile web
  * WebView

* iOS
  * mobile web
  * WebView

### Android

需準備的東西

* 電腦版的 chrome browser
* Android 手機(需要有 Android Chrome browser)

在 2018 年的當下這裡不想再提非 chrome browser 的開發, 因為很難 debug

以下就簡單說明一下

#### 1. 首先得把 Android 手機的開發者模式打開

**設定** -> **關於手機** -> **軟體版本**

找到**軟體版本**的選項就一直點, 直到點出提示您現在已成為開發人員, 這樣就可以了

進去**開發人員選項** 把 **USB 偵錯模式** 打開

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2FCapture%2B_2018-10-14-22-28-13.png?alt=media&token=cf2e0e3c-296d-45ee-a10c-0ac00ce13864)

#### 2. 連接手機到電腦

#### 3. 允許金鑰授權

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2FScreenshot_2018-10-11-15-36-36.png?alt=media&token=57443793-b3ea-464e-82c6-7568413a26f7)

#### 4. 打開電腦 chrome browser

#### 5. 打開 `開發人員工具`(Mac: `Command` + `Option` + `i`, PC: `F12`)

#### 6. 打開 `remove device`

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202018-10-10%20%E4%B8%8B%E5%8D%887.19.23.png?alt=media&token=d85970c0-613a-4f08-9a2f-020cebf8c227)

#### 7. 確認連接的裝置

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2018-10-11_%E4%B8%8B%E5%8D%884_13_29.png?alt=media&token=d0310aab-d4b7-4f03-b80e-cd29e3c5bc0d)

#### 8. 選擇 Inspect

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202018-10-11%20%E4%B8%8B%E5%8D%884.10.12.png?alt=media&token=dbf559eb-a83c-4862-af71-e8b1c627cee5)

[Refer - Get Started with Remote Debugging Android Devices](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)

#### 9. 開始 debug

#### Notice

Webiew 的部分需要注意的就是必須是 Android WebView 的 debug 是打開的

[Refer - Remote Debugging WebViews](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/webviews)


### iOS

需準備的東西

* Mac 的 Safari browser
* iPhone 手機

iPhone 目前只能針對 Safari debug, 其他 Browser 都沒辦法 debug

#### 1. 把 iPhone Safari 的開發者模式打開

**設定** -> **Safari** -> **進階**

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2FIMG_0311.PNG?alt=media&token=4999363b-a40a-4940-9a33-ed9bdc38864f)

JavaScript On

網頁檢閱器 On

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2FIMG_0310.PNG?alt=media&token=6efccdcc-f6e3-4932-806c-07daa5a828b7)

#### 2. 把 Mac Safari 的開發模式打開

**偏好設定** -> **進階** -> **在選單列中顯示「開發」選單**

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202018-10-11%20%E4%B8%8B%E5%8D%884.42.51.png?alt=media&token=55415544-998f-4bf2-b187-28572d933a8b)

#### 3. 連接手機到電腦

#### 4. 選擇信任這台電腦

#### 5. 打開電腦 Safari browser

#### 6. 到選單列 -> **開發** 確認 iPhone 已經顯示出來

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202018-10-11%20%E4%B8%8B%E5%8D%884.59.47.png?alt=media&token=1fab5a46-044a-40d7-a6a6-032135393c7f)

#### 7. 選擇要 debug 的網址

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202018-10-11%20%E4%B8%8B%E5%8D%885.13.50.png?alt=media&token=45048bb1-d2a4-4cb5-923e-7ea9477021d9)

#### 8. 開始 debug

#### Notice

iOS 的 debug 只有 beta 和 Xcode building 出來的 App 會出現, 線上版不會出現

在選單中不會分出該 url 是 WebView 或 browser 的 url, 且有時頁面關掉還會在選單中存在, 所以要仔細確認

### 最後

還有二個在 WebView 勉強可以稍微 debug 的方法

1. 掛 proxy

可以看到手機上的的 Network 情況

2. Xcode or Android studio log

上述兩種方法對 WebView 所能做的 debug 有限

PPT

[HackMD](https://hackmd.io/_Zte5OdFT5OhhO72BoTp-A)
