---
layout: post
title: 'JavaScript - Dynamic Load script || JSONP Callback'
date: 2015-06-08
comments: true
categories: [javascript, Ajax, jsonp]
---
## JavaScript - Dynamic Load script || JSONP Callback

### Intro

Sometimes we need dynamic load script or handle jsonp callback

And we need handle script onload or jsonp callback onload or something error

### How to do?

Use `onload`, `onerror` method

### Code

```javascript
if (typeof UTIL == 'undefined' || !UTIL) {
    var UTIL = {};
}
UTIL.createEl = {
    get: function(sTag, oAttr, handleOnLoad, handleError) {
        var el = document.createElement(sTag);
        for (var i in oAttr) {
            el[i] = oAttr[i];
        }
        if (handleOnLoad) {
            el.onload = handleOnLoad;
        }
        if (handleError) {
            el.onerror = handleError;
        }
        this.append(el);
        return el;
    },
    append: function(dNode) {
        var dHead = document.getElementsByTagName('head')[0] || document.body;
        dHead.appendChild(dNode);
    },
    remove: function(dNode) {
        setTimeout(function() {
            dNode.parentNode.removeChild(dNode);
            dNode = null;
        }, 0);
    },
    js: function(sUrl, handleOnLoad, handleError) {
        var dNode = this.get('script', {
            src: sUrl,
            type: 'text/javascript'
        }, handleOnLoad, handleError);
        return dNode;
    },
    css: function(sUrl, sMedia) {
        if (!sMedia) {
            sMedia = 'all';
        }
        return this.get('link', {
            'href':sUrl,
            'rel':'stylesheet',
            'type':'text/css',
            'media':sMedia
        });
    }
};
```

### Example

```javascript
var run = function() {
    alert('OK');
},
errorHandle = function() {
    alert('Error');
};
UTIL.createEl.js('http://tysh310246.blogspot.com/feeds/posts/default?alt=json&callback=myFunction', run, errorHandle);

function myFunction (data) {
    console.log(data);
}
```

[Refer - JavaScript Madness: Dynamic Script Loading](http://unixpapa.com/js/dyna.html)
[Refer - Script Loading issue « 小莊記事](http://www.kvzhuang.net/posts/245327-script-loading-issue)
