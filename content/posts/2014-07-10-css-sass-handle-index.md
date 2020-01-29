---
layout: post
title: 'CSS - SASS handle index'
date: 2014-07-10
comments: true
categories: [css, sass]
---
## CSS - SASS handle index

Can use var control z-index

```css
$elements: con, slider, masthead;

.masthead {
  /* z-index: 3 */
  z-index: index($elements, masthead);
}

.slider {
  /* z-index: 2 */
  z-index: index($elements, slider);
}

.con {
  /* z-index: 1 */
  z-index: index($elements, con);
}
```

[Refer - 使用 sass 有效控管 z-index 圖層順序](http://blog.mukispace.com/sass-z-index-management/)
