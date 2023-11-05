---
title: "CSS 處理多行省略"
date: 2023-11-06T00:43:26+08:00
draft: false
categories: [css]
---

```CSS
.multiline-ellipsis {
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3; /* start showing ellipsis when 3rd line is reached */
  white-space: pre-wrap; /* let the text wrap preserving spaces */
}
```


[refer - Easiest Way to Truncate Text With Ellipsis in CSS](https://codefrontend.com/css-ellipsis/)