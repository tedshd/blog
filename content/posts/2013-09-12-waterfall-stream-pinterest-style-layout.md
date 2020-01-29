---
layout: post
title: '瀑布流(Pinterest-style) layout'
date: 2013-09-12
comments: true
categories: [css javascript]
---
## 瀑布流(Pinterest-style) layout

目前看見 3 種作法

* jquery plug in
* salvattore.js
* CSS3 column

## jquery plug in

### Masonry

一款較多人使用的 jQuery plug in, 可向下相容到 IE8
[Masonry](http://masonry.desandro.com/)

### Grid-A-Licious

jQuery plug in, 向下相容到 IE9
[Grid-A-Licious](https://github.com/suprb/Grid-A-Licious)

## salvattore

利用 data attribute 來達到 CSS3 column 的效果
獨立運作的 js 不必依靠其他的 js library
輕巧快速
向下相容到 IE9
[salvattore](http://salvattore.com/)
不過沒 CSS 所以要加入 CSS 以便讓版面順利出來
已修改的 [salvattore](https://github.com/tedshd/salvattore)
CSS source code(可依需求進行修改)
```css
@-webkit-keyframes showsup {
  from { opacity: 0; -webkit-transform: translate(0, -20px); }
  to   { opacity: 1; -webkit-transform: translate(0, 0); }
}
@-moz-keyframes showsup {
  from { opacity: 0; -moz-transform: translate(0, -20px); }
  to   { opacity: 1; -moz-transform: translate(0, 0); }
}
@-o-keyframes showsup {
  from { opacity: 0; -o-transform: translate(0, -20px); }
  to   { opacity: 1; -o-transform: translate(0, 0); }
}
@keyframes showsup {
  from { opacity: 0; transform: translate(0, -20px); }
  to   { opacity: 1; transform: translate(0, 0); }
}

.salvattore-grid-b .item.added {
  -webkit-animation: showsup 0.5s;
  -moz-animation: showsup 0.5s;
  -o-animation: showsup 0.5s;
  animation: showsup 0.5s;
}

.layout-redux {
  width: 75%;
  margin-left: auto;
  margin-right: auto;
}

.column {
  float: left;
  width: 100%;
}

.one-half {
  width: 50%;
}
.one-third {
  width: 33.333%;
}
.one-quarter {
  width: 25%;
}
.hide {
  display: none;
}

@media screen and (max-width: 480px) {
  body {
    padding: 0 20px;
    font-size: 14px;
  }
  .rs-font-alpha, h1 {
    font-size: 36px;
  }

  .rs-font-beta {
    font-size: 24px;
  }

  .rs-font-gamma {
    font-size: 18px;
  }

  .rs-font-delta {
    font-size: 18px;
  }

  .branding {
    font-size: 72px;
  }
  .layout-redux {
    width: inherit;
  }
}
@media screen and (min-width: 481px) and (max-width: 768px) {
  body {
    font-size: 16px;
  }
  .rs-font-alpha, h1 {
    font-size: 48px;
  }

  .rs-font-beta {
    font-size: 36px;
  }

  .rs-font-gamma {
    font-size: 24px;
  }

  .rs-font-delta {
    font-size: 24px;
  }

  .branding {
    font-size: 96px;
  }

  .layout-redux {
    width: inherit;
  }
}

/* Grids */
.salvattore-grid,
.salvattore-grid-b {
  margin: 0 -10px;
}

[data-columns]:before {
  display: none;
}

.salvattore-grid[data-columns]:before {
  content: '4 .column.one-third';
}
.salvattore-grid-b[data-columns]:before {
  content: '3 .column.one-half';
}

@media screen and (max-width: 480px){
  .salvattore-grid[data-columns]:before,
  .salvattore-grid-b[data-columns]:before {
    content: '1';
  }
}

@media screen and (min-width: 481px) and (max-width:819px) {
  .salvattore-grid[data-columns]:before {
    content: '2 .column.one-half';
  }
}
@media screen and (min-width: 820px) and (max-width: 1299px) {
  .salvattore-grid[data-columns]:before {
    content: '3 .column.one-third';
  }
}
@media screen and (min-width: 1300px){
  .salvattore-grid[data-columns]:before {
    content: '4 .column.one-quarter';
  }
}

@media screen and (min-width: 481px) and (max-width: 1099px) {
  .salvattore-grid-b[data-columns]:before {
    content: '2 .column.one-half';
  }
}
@media screen and (min-width: 1100px) {
  .salvattore-grid-b[data-columns]:before {
    content: '3 .column.one-third';
  }
}
```

[codepen - demo](https://codepen.io/tedshd/pen/YMpGVo)

[demo2](https://codepen.io/tedshd/pen/YzzazKp)

## CSS3 column

依情況需作 responsive web design
不然 layout 在做縮放會跑掉

CSS 必須調整好
```css
/*--指定分欄數量--*/
.col {
    column-count: 2;
    -webkit-column-count: 2;
    -moz-column-count: 2;
}
/*--指定分欄寬度(預設 auto)--*/
.col {
    column-width: 50px;
    -webkit-column-width: 50px;
    -moz-column-width: 50px;
}
```

HTML 依照下面的寫法
```html
<ul class="col">
    <li>
        <!-- do something -->
    </li>
    <li>
        <!-- do something -->
    </li>
    <li>
        <!-- do something -->
    </li>
</ul>
```
[Html5(css3)的瀑布流布局的实现](http://www.niumowang.org/html-css/html5-css3-waterfall/)

[codepen - demo](https://codepen.io/tedshd/pen/zYYWaWM)
