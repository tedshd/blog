---
layout: post
title: 'CSS - 垂直置中'
date: 2014-04-07
comments: true
categories: [css]
---
## CSS - 垂直置中

### 文字垂直置中

之前 ApplyBOY 在網路上分享了一個 CSS 垂直置中的一個解法
這裡整理出個小小模組出來

假如那一個區域內的東西需做垂直置中, 在該區域的 element 加上 class `vertical-centering`

```css
.vertical-centering:before {
  content: '';
  display: inline-block;
  vertical-align: middle ;
  height: 100%;
}
```

該區域的文字就會垂直置中

**Example**

<p data-height="268" data-theme-id="2982" data-slug-hash="vGtrA" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/tedshd/pen/vGtrA/'>vertical-centering</a> by Ted (<a href='http://codepen.io/tedshd'>@tedshd</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

### 區域垂直置中

如要在一區域內有一小塊區域置中則需把該區域做 `vertical-align: middle;`

```css
.vertical-centering-area {
  vertical-align: middle;
}

.vertical-centering:before {
  content: '';
  display: inline-block;
  vertical-align: middle ;
  height: 100%;
}
```

**Example**

<p data-height="268" data-theme-id="2982" data-slug-hash="Ckopr" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/tedshd/pen/Ckopr/'>vertical centering area</a> by Ted (<a href='http://codepen.io/tedshd'>@tedshd</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>


[Refer - CSS 垂直置中解法](http://blog.wu-boy.com/2013/07/css-vertical-align-center/)
