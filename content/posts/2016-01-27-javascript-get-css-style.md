---
layout: post
title: 'JavaScript - get CSS style'
date: 2016-01-27
comments: true
categories: [javascript, css]
---
## JavaScript - get CSS style

Sometimes i want to use JavaScript get dom CSS style.

Use `DOM.currentStyle` and `window.getComputedStyle(DOM)`

For IE use **DOM.currentStyle**

Other use **window.getComputedStyle(DOM)**

```javascript
var dom = document.getElementById("target"),
    style = dom.currentStyle || window.getComputedStyle(dom);
console.log(style.marginTop);
```


[refer - Window.getComputedStyle() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/getComputedStyle)

[refer - currentStyle object (Internet Explorer)](https://msdn.microsoft.com/en-us/library/ms535231(v=vs.85).aspx)
