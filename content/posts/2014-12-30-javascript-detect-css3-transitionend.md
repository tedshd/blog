---
layout: post
title: 'JavaScript - detect CSS3 transitionEnd'
date: 2014-12-30
comments: true
categories: [javascript, css, css3]
---
## JavaScript - Detect CSS3 transitionEnd

[transitionend](https://developer.mozilla.org/en-US/docs/Web/Events/transitionend)

It is a event can fired when CSS3 transition end.

```javascript
function transitionEnd() {
    var el = document.createElement('div'), //what the hack is bootstrap
        transEndEventNames = {
        WebkitTransition : 'webkitTransitionEnd',
        MozTransition    : 'transitionend',
        OTransition      : 'oTransitionEnd otransitionend',
        transition       : 'transitionend'
    };

    for (var name in transEndEventNames) {
        if (el.style[name] !== undefined) {
            return transEndEventNames[name];
        }
    }

    return false; // explicit for ie8 (  ._.)
}

// Usage
document.querySelector('body').addEventListener(transitionEnd(), function () {
// dosomething
});
```

[Refer - Easy way to detect support for transitionend event without frameworks like jQuery or Modernizr?](http://stackoverflow.com/questions/19635986/easy-way-to-detect-support-for-transitionend-event-without-frameworks-like-jquer)
