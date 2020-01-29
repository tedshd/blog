---
layout: post
title: 'JavaScript - handle textarea value'
date: 2014-10-01
comments: true
categories: [javascript]
---
## JavaScript - handle textarea value

Handle textarea string.

```javascript
// jQuery
var textarea = $('textarea').val().replace(/\n/g, '<br>');
// JavaScript
var textarea = document.querySelector('textarea').value.replace(/\n/g, '<br>');
```
