---
layout: post
title: 'JavaScript - Event'
date: 2013-11-09
comments: true
categories: [javascript]
---
## JavaScript - Event

* event type
事件名稱

* event target
事件發生在哪一個目標上

* event handler or listener
處理或回應的 function, 即監聽或註冊事件

* event object
與事件關聯的物件

* event propagation
氣泡(bubble)現象

* default actions
觸發事件時的預設行為, 有時必須取消該行為


### [GlobalEventHandlers](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers)

* HTML
```html
<button id="btn">Click</button>
```

* JavaScript
```javascript
var nodeBtn = document.getElementById('btn');
nodeBtn.onclick = function (e) {
    alert('ok');
};
```

### event

* HTML
```html
<button id="btn">Click</button>
```

Use addEventListener(only IE9 up)
[addEventListener](https://developer.mozilla.org/zh-CN/docs/DOM/element.addEventListener)

* JavaScript
```javascript
var nodeBtn = document.getElementById('btn');
nodeBtn.addEventListener('click', function () {
    alert('ok');
});
```

### delegate

If use dynamic page the dom maybe not init in the page load
So use delegate

```javascript
var div = document.createElement('div'),
    prefix = ['moz','webkit','ms','o'].filter(function (prefix) {
        return prefix + 'MatchesSelector' in div;
    })[0] + 'MatchesSelector';

Element.prototype.addDelegateListener = function(type, selector, fn) {
    this.addEventListener( type, function(e) {
        var target = e.target;

        while(target && target !== this && !target[prefix](selector)) {
            target = target.parentNode;
        }
        if(target && target !== this) {
            return fn.call(target, e);
        }
    }, false );
};
```

* example

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>javascript - delegate</title>
</head>
<body>

</body>
<script>
var div = document.createElement('div'),
    prefix = ['moz','webkit','ms','o'].filter(function (prefix) {
        return prefix + 'MatchesSelector' in div;
    })[0] + 'MatchesSelector';

Element.prototype.addDelegateListener = function(type, selector, fn) {
    this.addEventListener( type, function(e){
        var target = e.target;

        while(target && target !== this && !target[prefix](selector)) {
            target = target.parentNode;
        }
        if(target && target !== this) {
            return fn.call(target, e);
        }

    }, false );
};

document.querySelector('body').addDelegateListener('click', '#btn', function () {
    alert('ok');
});

document.body.innerHTML = '<button id="btn">Click</button>';
</script>
</html>
```

[Refer - addEventListener for new elements](http://stackoverflow.com/questions/11179841/addeventlistener-for-new-elements)

[Refer - 為什麼有時你應該優先考慮 event delegate 而不是 event binding](http://ithelp.ithome.com.tw/question/10120565?tag=ithome.nq)

[Refer - An Introduction To DOM Events](http://coding.smashingmagazine.com/2013/11/12/an-introduction-to-dom-events/)
