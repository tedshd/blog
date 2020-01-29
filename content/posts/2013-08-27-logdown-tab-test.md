---
layout: post
title: 'logdown Tab test'
date: 2013-08-27
comments: true
categories:
---
## Tab problem

### Problem

Mac 的 function 中 console.log('hihi') 是按一次 Tab 有 4 個空白
but
alert('hihi') 這一行在按 Tab 縮排就有問題，再接續上一行按 enter 下來之後縮排剩 2 個空白，之後再按 Tab 縮排會變成只有 2 個空白
在 fun2 的 function 中都是直接按 4 個空白鍵來作縮排，都正常

### 發生現象
在按 Tab 縮排過，打完那一行直接按 enter 到下一行，縮排就從 4 個空白變成 2個空白

### 期望
希望用 Tab 時在 Edit 和 Preview(最終結果)的結果是一樣的

```javascript
var Mac = function() {
	console.log('hihi');
  if (!console) {
  	alert('hihi');
  }
}
var fun function() {
	console.log(1);
  console.log(2);
	console.log('reset 重新從最左邊按一次 Tab');
}
var fun2 = function() {
    console.log('hihi');
    condsole.log('ok');
    if (fun) {
        console.log('good');
    }
}
```
