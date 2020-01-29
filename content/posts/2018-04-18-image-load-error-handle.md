---
layout: post
title: 'HTML - image load error handle'
date: 2018-04-18
comments: true
categories: [HTML image]
---
## HTML - image load error handle

2 way

### Use `onerror`

```html
<img src="<image url>" onerror="this.src='<d4 image url>'" />
```

### Use Magic Image Pseudo Element

```
img.imgd4 {
    position: relative;
    display: block;
}

img.imgd4:after {
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    background: url(<d4 image url>) no-repeat;
    background-size: contain;
    width: 100%;
    height: 100%;
    content: '';
}
```
