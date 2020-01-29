---
layout: post
title: 'JavaScript - insertBefore & insertAfter'
date: 2015-06-27
comments: true
categories: [javascript]
---
## JavaScript - insertBefore & insertAfter

### insertBefore

This is native JavaScript api

`var insertedElement = parentElement.insertBefore(newElement, referenceElement);`

```javascript
var vDom = document.createElement('div'),
    dom = document.querySelector('#list');
dom.insertBefore(vDom, dom.childNodes[1]);

// or

var vDom = document.createElement('div'),
    dom = document.querySelector('#target');
dom.parentNode.insertBefore(vDom, dom);
```

[Refer - Node.insertBefore()](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore)

### insertAfter

JavaScript doesn't have any api handle insert DOM after reference DOM

We can use this way

```javascript
function insertAfter(newNode, referenceNode) {
    referenceNode.parentNode.insertBefore(newNode, referenceNode.nextSibling);
}
```

[Refer - How to do insert After() in JavaScript without using a library?](http://stackoverflow.com/questions/4793604/how-to-do-insert-after-in-javascript-without-using-a-library)
