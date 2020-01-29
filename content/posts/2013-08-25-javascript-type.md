---
layout: post
title: 'JavaScript type'
date: 2013-08-25
comments: true
categories: [javascript]
---
## JavaScript Type

* number
* string
* boolean
* null
* undefind

減少 type 轉換以加快執行速度

## Object

### var

* 宣告後即擁有物件的屬性
* 宣告之後無法刪除
 * 區域變數

 function 內宣告
 * 全域變數

 小心使用

### property

* 建立在物件中
* 可刪除

## Array

* method 1

```javascript
var arr = new Array();
```
bug
```javascript
var arr = new Array(10);
arr
// [undefined × 10]
```

* method 2

```javascript
var arr = [];
```
