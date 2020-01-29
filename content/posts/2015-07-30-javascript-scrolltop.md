---
layout: post
title: 'JavaScript - scrollTop'
date: 2015-07-30
comments: true
categories: [javascript]
---
## JavaScript - scrollTop

### scrollTop

[Element.scrollTop - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollTop)

### Issue in firefox

Normal

```javascript
element.scrollTop = intValue;
```

But when I use

```javascript
document.body.scrollTop = 0;
```

It doesn't work in firefox.

Solution

```javscript
document.documentElement.scrollTop = 0; // for firefox
```

[Refer - document.body.scrollTop vs document.documentElement.scrollTop](https://miketaylr.com/posts/2014/11/document-body-scrollTop.html)
