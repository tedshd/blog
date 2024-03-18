---
title: "JavaScript 確認頁面有沒有縮放"
date: 2024-02-19T11:24:18+08:00
draft: false
categories: [JavaScript, mobile]
---

## 前言

不管在 mobile 還是 desktop 都有個困擾就是要處理用戶縮放頁面的問題

如果只是資料類型的頁面, 縮放的話大多都只是畫面 UI 跑版

但如果是複合功能型的頁面, 縮放的話大概率會讓功能壞掉

就得找一些方法處理

## 確認可行性

JavaScript 有一個 api `window.devicePixelRatio` 是顯示畫面解析度比率的

早期可以用這個是不是 1 來判斷

但是螢幕的解析度其實會影響這個值

所以這個 api 沒有辦法當作判斷的基準

`resize` 事件可以在頁面縮放時會觸發

搭配 `window.outerWidth/window.innerWidth` 的值的變化可以知道有沒有縮放

但是這在 mobile device 的兩指縮放是不會觸發

所以也沒用...

但是針對 mobile 兩指縮放

可以使用 `window.visualViewport`

`window.visualViewport.scale` 可以知道現在縮放比例

如果只是要判斷有沒有所放的話

可以使用 `resize` 事件 + mobile 判斷來拿取 `window.visualViewport.scale` 或是 `let zoom = window.outerWidth/window.innerWidth;` 的組合來處理

sample code

```javascript
let zoom = window.outerWidth / window.innerWidth;

function isMobileDevice() {
    return /Mobi/i.test(navigator.userAgent);
}

function handleZoom() {

    if (isMobileDevice()) {
        if ('visualViewport' in window) {
            zoom = window.visualViewport.scale;
        } else {
            zoom = window.outerWidth / window.innerWidth;
        }
    } else {
        zoom = window.outerWidth / window.innerWidth;
    }

    console.log("Zoom level: " + zoom);
}

window.addEventListener('resize', handleZoom);

handleZoom();
```

[refer - 如何使用JS檢測使用者是否縮放了頁面？](https://www.zhangxinxu.com/wordpress/2021/02/js-if-page-zoom/)