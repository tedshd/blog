---
layout: post
title: 'HTML Design Pattern'
date: 2013-08-21
comments: true
categories: [html]
---
## HTML Design Pattern

### 語意化(影響 SEO)
### 去 CSS 還可維持可讀性
### 去 JavaScript 頁面還能 work -> 現在較不適用
### 避免樣式標籤
```html
<!-- not recommended -->
<b></b>
<i></i>
<!-- use -->
<strong></strong>
<em></em>
```
### 避免將 style 寫在 HTML tag 上
### 善用標籤以維持可讀性與語意化
### 網頁上的載入圖片做適當的選擇
* 會變動的圖片以 ```<img src="">``` 呈現
* 幾乎不會變動或重要性要低的圖片適合以 background 呈現
* 適當的利用 CSS sprite
