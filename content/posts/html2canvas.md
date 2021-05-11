---
title: "Html2canvas"
date: 2020-09-03T16:05:40+08:00
draft: false
categories: ["canvas"]
---

## 網站直接網頁截圖

基本上就是把要截圖的內容轉成 canvas 物件

再轉成圖片下載即可

### 現成套件 html2canvas

https://html2canvas.hertzen.com/

但是如果要截圖的內容有用外部 url 載入的圖片需要注意一下 CORS 問題(canvas 的限制)

### 解決外部 url 載入圖片時 CORS 問題

原理

把外部載入的圖片轉換成二進制再轉成 dataurl

因為在 browser 上面可以解析與渲染 dataurl

所以就可以呈現在 canvas 裡面

這樣之後要截圖下載這個 canvas 的內容也沒問題

### 補充轉換圖片的機制(解決載入外部圖片 CORS 問題)

#### 處理方式 - 圖片轉 blob

圖片轉成 blob

```javascript
function toDataURL(url, callback) {
    var xhr = new XMLHttpRequest();
    xhr.onload = function() {
        var reader = new FileReader();
        reader.onloadend = function() {
            callback(reader.result);
        }
        reader.readAsDataURL(xhr.response);
    };
    xhr.open('GET', url);
    xhr.responseType = 'blob';
    xhr.send();
}
```

#### 問題(更新 2021/05/11)

CORS 問題越來越嚴格了

在瀏覽器上面 XMLHttpRequest 物件處理 binary 現在會有 CORS 問題要處理

需要在要處理的圖片 url 處理 CORS(圖片所在的 host 必須有允許 CORS 的 header)

[refer - Allowing cross-origin use of images and canvas](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_enabled_image)

[refer - 解决 canvas 将图片转为base64报错](https://www.jianshu.com/p/6fe06667b748)
