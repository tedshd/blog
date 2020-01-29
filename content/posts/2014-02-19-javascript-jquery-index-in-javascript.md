---
layout: post
title: 'JavaScript - jQuery index() in JavaScript'
date: 2014-02-19
comments: true
categories: [javascript]
---
## JavaScript - jQuery index() in JavaScript

### JavaScript

```javascript
function indexInParent(node) {
    var children = node.parentNode.childNodes;
    var num = 0;
    for (var i=0; i<children.length; i++) {
         if (children[i]==node) return num;
         if (children[i].nodeType==1) num++;
    }
    return -1;
}
```

### Example

```html
<ul>
  <li id="foo">foo</li>
  <li id="bar">bar</li>
  <li id="baz">baz</li>
</ul>
```

* jQuery

```javascript
alert($('#bar').index());
```

* javaScript

```javascript
var el = document.getElementById("bar");
function indexInParent(node) {
    var children = node.parentNode.childNodes;
    var num = 0;
    for (var i=0; i<children.length; i++) {
         if (children[i]==node) return num;
         if (children[i].nodeType==1) num++;
    }
    return -1;
}
alert(indexInParent(el));
```

[Demo](http://jsbin.com/yabapalu/1/)

[Refer - jQuery .index() in javascript](http://stackoverflow.com/questions/13658021/jquery-index-in-javascript)
