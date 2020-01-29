---
layout: post
title: 'JavaScript - something about childNodes and nextSibling why they get DOM is not as you imagine'
date: 2015-08-28
comments: true
categories: [javascript, DOM]
---
## JavaScript - something about childNodes and nextSibling why they get DOM is not as you imagine

[childNodes MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/childNodes)

[nextSibling - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/nextSibling)

### Sometimes we use childNodes

#### HTML

```html
<ul>
  <li>item1</li>
  <li>item2</li>
  <li>item3</li>
  <li>item4</li>
</ul>
```

#### JavaScript

```javascript
console.log(document.querySelector('ul').childNodes);
// output
[text, li, text, li, text, li, text, li, text]
```

![螢幕快照_2015-08-29_上午12_08_56.png](http://user-image.logdown.io/user/3170/blog/3202/post/293568/plBejfI1SXq1dBNPNyqr_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2015-08-29_%E4%B8%8A%E5%8D%8812_08_56.png)

Why?

Then

#### HTML

```html
<ul><li>item1</li><li>item2</li><li>item3</li><li>item4</li></ul>
```

#### JavaScript

```javascript
console.log(document.querySelector('ul').childNodes);
// output
[li, li, li, li]
```

![螢幕快照_2015-08-29_上午12_10_07.png](http://user-image.logdown.io/user/3170/blog/3202/post/293568/b7H4oj6ZTMeH5jt01zaT_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2015-08-29_%E4%B8%8A%E5%8D%8812_10_07.png)

If you log `text` object, you can find it is wrap.

![螢幕快照_2015-08-29_上午12_09_30.png](http://user-image.logdown.io/user/3170/blog/3202/post/293568/QKnxVI8fRGWaAS0fagqc_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2015-08-29_%E4%B8%8A%E5%8D%8812_09_30.png)

**Browser get nodes include wrap symbol.**

But it can't show in your editor

#### Solution

* for IE9 up

[ParentNode.children](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children)

* do a new function

```javascript
Element.prototype.getChildNodes = function () {
  var array = [],
      nodes = this.childNodes;
  for(var i = 0; i < nodes.length; i++) {
    var node = nodes[i];
    if (node.nodeType === Node.ELEMENT_NODE) {
      array.push(node);
    }
  }

  return array;
};
console.log(document.querySelector('ul').getChildNodes());
```

[HTML DOM nodeType Property](http://www.w3schools.com/jsref/prop_node_nodetype.asp)

* the way [rplus](https://www.facebook.com/rplus.tw) provide

```javscript
function getChildNodes(parentNode) {
  return [].filter.call(
    parentNode.childNodes,
    function(_target) {
      return _target.nodeType === Node.ELEMENT_NODE;
    });
}
```

### Sometimes we use nextSibling

As above

Sometimes you get `text`.
