---
layout: post
title: 'JavaScript - delete element'
date: 2014-03-13
comments: true
categories: [javascript]
---
## JavaScript - delete element

I use this way.

```javascript
var dom = document.querySelectorAll('.dom');

for (var i = 0; i < dom.length; i++) {
    dom[i].outerHTML = '';
    delete dom[i];
};

// or

var dom = document.querySelector('#dom');

var dom = document.querySelector('h1');

dom.outerHTML = '';
delete dom;
```

If use IE
`document.querySelector` only use IE8 up

[Refer - JavaScript: remove element by id](http://stackoverflow.com/questions/3387427/javascript-remove-element-by-id)
