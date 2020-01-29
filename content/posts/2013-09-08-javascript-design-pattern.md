---
layout: post
title: 'JavaScript - design pattern'
date: 2013-09-08
comments: true
categories: [javascript]
---
## JavaScript - design pattern

### 避免與減少全域變數(global variable)
全域變數非常方遍使用, 但使用的不好會使 JavaScript 有問題
因為有可能重複使用且有可能別的 library 也有用到該名稱
在 __*JavaScript: 優良部分*__ 書中提到可用物件的方式包起來

```javascript
var GlobalObj = {};
// 開始定義
GlobalObj.var1 = 'string';
GlobalObj.arr = [1, 2, 3];
...

// or
var GlobalObj = {
        var1: 'string',
        arr: [1, 2, 3]
    };
```

使用 **閉包(Closure)** 也是一個避免全域變數的方法
