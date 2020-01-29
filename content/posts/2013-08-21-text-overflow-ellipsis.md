---
layout: post
title: '文字過多時省略(ellipsis)'
date: 2013-08-21
comments: true
categories: [css]
---
## text ellipsis

```css
div {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    width: 240px;
}
```

### Tip
上述為必要
element 必須為 block
如用在 span 等行內元素，需用 display: inline-block;
**多行會變一行顯示**
