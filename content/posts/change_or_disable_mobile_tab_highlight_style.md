---
title: "調整和關閉 mobile device 點擊時 highligh 樣式"
date: 2022-06-29T11:41:23+08:00
draft: false
categories: [CSS]
---

mobile web 會在點擊 a link 的時候 highlight 那個部分

原意是為了讓使用者更能夠直觀地知道是否有點擊了那個東西

但是有時這個樣式會和整體 web 的設計不合

所以會想辦法改變或關掉這個 highlight

那就得使用一個 CSS 屬性 `-webkit-tap-highlight-color`

如果要關掉, 那就改成透明的

```CSS
-webkit-tap-highlight-color: transparent;
```

如果要改成別的顏色就設定顏色即可

```CSS
-webkit-tap-highlight-color: red;
```

[-webkit-tap-highlight-color MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/-webkit-tap-highlight-color)