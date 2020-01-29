---
layout: post
title: 'JavaScript - 計算網頁元件的曝光'
date: 2018-11-21
comments: true
categories: [JavaScript]
---
## JavaScript - 計算網頁元件的曝光

因為某些需求需要精確計算某些網頁上的 UI 元件的曝光

沒錯

就是要像廣告計算 impression 一樣

之前只要確認有該元件的 request 就好了

但是為了精確追求計算曝光, 所以必須做到像 Google Ad 一樣

要到該網頁元件讓使用者看到後才能計算曝光

聽起來這要求不太容易

但是實作下去其實發現還好誒!!

### 概念

DOM 元件進入可視範圍觸發 impression

所以需要能夠釐清一些問題

1. 如何確認可視範圍?

2. 如何確認要記錄 impression 的 DOM 元件在可視範圍?

3. 如何在進入可視範圍時觸發?

看似困難

但是如果熟悉 JavaScript Window 物件和 DOM 物件的話就會發現很好解

### 實作

#### 如何確認可視範圍?

```JavaScript
window.document.documentElement.clientHeight

window.document.documentElement.clientWidth
```

完美解決

#### 如何確認要記錄 impression 的 DOM 元件在可視範圍?

```
<DOM Object>.getBoundingClientRect();
```

完美解決

但是要取到對應可是範圍的位置建議使用(`top`, `left`), `x` `y` IE 和 Edge 不支援

還有一點要注意就是該 DOM 要先長在 browser 上面且不是 `display: none` 的狀態才能拿到值

[Refer - Element.getBoundingClientRect() - Web API 接口 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect)

[Refer - ClientRect object (Internet Explorer)](https://msdn.microsoft.com/en-us/library/hh826029(VS.85).aspx)

#### 如何在進入可視範圍時觸發?

這就得取決於使用情境了

在適當的 Event 去觸發

Ex:

在 list view 時就單純的用 scroll 事件觸發確認是否是進入可視範圍(當然得做 debounce 處理)

在 carousel view 就滑動或點擊觸發轉動時確認是否是進入可視範圍(如果有做動畫效果, 得等到動畫效果結束再去確認)

### 結論

熟悉基本 API 後就可以很輕鬆地解決很多問題 XD

最後附上包好的套件

[GitHub - impression](https://github.com/tedshd/impression)
