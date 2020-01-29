---
layout: post
title: 'JavaScript - 半形 全形 轉換'
date: 2019-01-30
comments: true
categories: [JavaScript]
---
## JavaScript - 半形 全形 轉換

因為一個奇怪的需求?

需要把使用者輸入的東西轉成可以方便驗證的格式(這應該後端做吧?)

反正因為以前也做過半形轉成全形(痛苦的回憶, 為啥政府的 opendata 各縣市格式不一致就算了, 竟然還有全形半形的問題...)

這邊就簡單的只針對最前面的基本拉丁字母字元符號集作轉換

因為大部分的需求應該這樣就可以應付了?

但是空白字元要特殊處理

那接下來只要知道需要轉換的字元範圍即可

全形從 `U+FF01` 到 `U+FF5E`

半形從 `U+0021` 到 `U+007E`

把 16 進制轉換回來就是

65281 到 65374

33 到 126

上述怎麼轉的?

就是這樣

```JavaScript
parseInt('0xFF01', 16)
```

只要判斷輸入的字元這這些編碼區間就進行轉換

[trans char](https://tedshd.io/demo/trans.html)

所以簡單做了一個 demo 頁面

程式檢視原始碼即可

[Refer - Wiki](https://zh.wikipedia.org/wiki/%E5%85%A8%E5%BD%A2%E5%92%8C%E5%8D%8A%E5%BD%A2)

[Refer - Unicode / UTF-8 字元編碼區間表 - 2013](https://blog.longwin.com.tw/2013/12/unicode-utf8-char-range-table-2013/)
