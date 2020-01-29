---
layout: post
title: 'Konami 密技 JavaScript 簡單實作'
date: 2013-12-19
comments: true
categories: [javascript]
---
## Konami 密技 JavaScript 簡單實作

最近有一個網站很紅
[vogue](http://www.vogue.co.uk/)
上上下下左右左右BA
接下來就狂按 A

[KONAMI 密技](http://zh.wikipedia.org/zh-tw/%E7%A7%91%E4%B9%90%E7%BE%8E%E7%A7%98%E6%8A%80)阿

身為一個宅宅前端攻城獅一定要學起來這招(~~以後就藏一些東西在程式中~~)

[Demo](http://tedshd.lionfree.net/demo/konami.html)

```javascript
    var keyCount = 0;
    window.onkeydown = konami;
    function konami(e) {
        if (e.keyCode === 38 && keyCount === 0) {
            keyCount++;
            console.log(keyCount);
        } else if (e.keyCode === 38 && keyCount === 1) {
            keyCount++;
            console.log(keyCount);
        } else if (e.keyCode === 40 && keyCount === 2) {
            keyCount++;
            console.log(keyCount);
        } else if (e.keyCode === 40 && keyCount === 3) {
            keyCount++;
            console.log(keyCount);
        } else if (e.keyCode === 37 && keyCount === 4) {
            keyCount++;
            console.log(keyCount);
        } else if (e.keyCode === 39 && keyCount === 5) {
            keyCount++;
            console.log(keyCount);
        } else if (e.keyCode === 37 && keyCount === 6) {
            keyCount++;
            console.log(keyCount);
        } else if (e.keyCode === 39 && keyCount === 7) {
            keyCount++;
            console.log(keyCount);
        } else if (e.keyCode === 66 && keyCount === 8) {
            keyCount++;
            console.log(keyCount);
        } else if (e.keyCode === 65 && keyCount === 9) {
            keyCount = 0;
            console.log('Konami');
            alert('打密技阿你');
        } else {
            keyCount = 0;
            console.log('fail');
        }
    }
```
