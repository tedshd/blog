---
layout: post
title: 'JavaScript - 多行文字省略'
date: 2014-05-30
comments: true
categories: [javascript]
---
## JavaScript - 多行文字省略

Sample code

* CSS

```css
.ellipsis-mult {
  width: 300px;
  height: 5em;
  overflow: hidden;
}
p {
    margin: 0;
}
```

* HTML

```html
<div class="ellipsis-mult">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nisi ligula, dapibus a volutpat sit amet, mattis et dui. Nunc porttitor accumsan orci id luctus. Phasellus ipsum metus, tincidunt non rhoncus id, dictum a lectus. Nam sed ipsum a lacus sodales eleifend. Vestibulum lorem felis, rhoncus elementum vestibulum eget, dictum ut velit. Nullam venenatis, elit in suscipit imperdiet, orci purus posuere mauris, quis adipiscing ipsum urna ac quam.</p>
</div>
```

* JavaScript

```javascript
var h = document.querySelector('.ellipsis-mult').clientHeight;
while (document.querySelector('.ellipsis-mult p').clientHeight > h) {
    var text = document.querySelector('.ellipsis-mult p').textContent;
    document.querySelector('.ellipsis-mult p').innerHTML = text.replace(/\W*\s(\S)*$/, '...');
}
```

[Refer - With CSS, use “…” for overflowed block of multi-lines](http://stackoverflow.com/questions/6222616/with-css-use-for-overflowed-block-of-multi-lines)
