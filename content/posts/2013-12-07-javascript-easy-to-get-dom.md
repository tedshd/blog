---
layout: post
title: 'JavaScript - Easy to get DOM'
date: 2013-12-07
comments: true
categories: [javascript]
---
## JavaScript - Easy to get DOM

It is old way to use ```getElementById```, ```getElementsByTagName``` ...

New method is use [querySelector](https://developer.mozilla.org/en-US/docs/Web/API/Document.querySelector) and [querySelectorAll](https://developer.mozilla.org/en-US/docs/Web/API/Document.querySelectorAll)

If use IE, it only for IE8 up.

Make them as a method

```javascript
var node;
function node(selector) {
    if (selector.indexOf('.') === -1) {
        if (document.querySelectorAll(selector).length === 1) {
            return document.querySelector(selector);
        }
        return document.querySelectorAll(selector);
    }
    return document.querySelectorAll(selector);
}
```

And then use it

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>querySelector</title>
</head>
<body>
    <div id="box" class="area">
        test
    </div>
    <div class="area">
        test2
    </div>
    <div id="selector" class="area">
        <p class="con">
            content
        </p>
    </div>
</body>
<script>
var node;
function node(selector) {
    if (selector.indexOf('.') === -1) {
        if (document.querySelectorAll(selector).length === 1) {
            return document.querySelector(selector);
        }
        return document.querySelectorAll(selector);
    }
    return document.querySelectorAll(selector);
}

console.log('ID', node('#box'));
console.log('CLASS', node('.area'));
console.log('SELECTOR_1', node('#selector p'));
console.log('SELECTOR_2', node('.area .con'));
</script>
</html>
```
