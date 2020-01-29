---
layout: post
title: 'innerHeight & innerWidth'
date: 2013-08-03
comments: true
categories: [javascript]
---
## innerHeight & innerWidth
抓取瀏覽器目前顯示高度與寬度
一般都用
```javascript
window.innerHeight
```
與
```javascript
window.innerWidth
```
但唯獨IE6~IE8不行
Google了一下
發現用
```javascript
window.document.documentElement.clientHeight
```
與
```javascript
window.document.documentElement.clientWidth
```
便兼容所有瀏覽器

## scrollHeight

如要抓 document 的高可用
```javascript
document.body.scrollHeight
```

[Refer](http://stackoverflow.com/questions/1145850/get-height-of-entire-document-with-javascript)
