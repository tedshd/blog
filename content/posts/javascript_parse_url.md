---
title: "Javascript 判斷並且取出 url"
date: 2022-01-04T16:04:04+08:00
draft: false
categories: [javascript, regex]
---

因為工作上的需要

需要把使用者輸入的訊息中含有 url 的部分把它取出來轉成超連結

參照以下範例

https://gist.github.com/metafeather/202974/34c2d31bd82f59c2486f38790054bbbc0b10ca8b

不知為何他的正規有點問題

所以又做了修正

```javascript
function urlParse(str) {
  var urlArray = [];
  var urlRegex = /((http[s]?|ftp):\/)\/?([^:\/\s]+)(?::([0-9]+))?((\/\w+)*\/)?([\w\-\.]*)?([#?\w\=]+)?([\&\w=\w]+.*)?([\w\+\-\/\%]*)?[A-Za-z0-9_\/]/g;
  var arr = str.split(/[\n,' ']+/gm);
  for (let u = 0; u < arr.length; u++) {
    const element = arr[u];
    var validate = element.match(urlRegex);
    if (validate) {
      urlArray.push(validate[0]);
    }
  }
  return urlArray;
}
```

url 格式遵循 RFC3986

[refer - rfc3986](https://datatracker.ietf.org/doc/html/rfc3986)

這邊可以在實作一個白名單機制限制只有白名單中的域名所屬的 url 才可以轉成超連結

```javascript
function urlWhitrList(url) {
  var list = [
    'www.instagram.com/',
    'youtu.be/',
    'www.youtube.com/',
    'www.facebook.com/',
    't.me/',
    'twitter.com/',
  ];
  for (let w = 0; w < list.length; w++) {
    const element = list[w];
    if (url.indexOf(element) !== -1) {
      return true;
    }
  }
  return false;
}
```

只要把這兩個 function 去檢查訊息的字串在做取代就可以把訊息字串中藥轉換的連結換成超連結了