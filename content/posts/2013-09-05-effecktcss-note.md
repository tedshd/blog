---
layout: post
title: 'Effeckt.css - Note'
date: 2013-09-05
comments: true
categories: [css]
---
## Effeckt.css

[demo](http://h5bp.github.io/Effeckt.css/dist/)

上面頁面都是利用 CSS3 的 Animations 與 Transitions 效果做出來的

[GitHub](https://github.com/h5bp/Effeckt.css)

使用該 library 須載入 [Modernizr](http://modernizr.com/) 這個 library
Modernizr 是用來判斷 browser 是否支援 HTML5 or CSS3 所用的 library, 並能把相同功能但在不同 browser 實作的 API 或 CSS3 property 一致化

主要是透過添加 class or data attribute 的方式, Modernizer 就在其中做了整合各 browser 的事情

### How does it work

動畫部分是利用 CSS3 的 Animations 與 Transitions
至於事件的觸發是利用 [CSS3 Transition Events](http://www.w3.org/TR/css3-transitions/#transition-events-), 由於各個 browser 實作都不一樣, 所以這裡加載了一個 ```/js/demo/demo.js``` 的 js, 但在這 js 有個有趣的地方就是有用 ajax 去載入開發者名單, 所以就另開個 js 來載入

**CSS3-event.js**
```javascript
var EffecktDemos = {

  init: function() {

    $(window).load(function() {
      $(".no-transitions").removeClass("no-transitions");
    });

    EffecktDemos.transitionEndEventName = EffecktDemos.transitionEndEventNames[Modernizr.prefixed('transition')];
    EffecktDemos.animationEndEventName = EffecktDemos.animationEndEventNames[Modernizr.prefixed('animation')];

  },

  animationEndEventNames: {
    'WebkitAnimation' : 'webkitAnimationEnd',
    'OAnimation' : 'oAnimationEnd',
    'msAnimation' : 'MSAnimationEnd',
    'animation' : 'animationend'
  },

  transitionEndEventNames: {
    'WebkitTransition' : 'webkitTransitionEnd',
    'OTransition' : 'oTransitionEnd',
    'msTransition' : 'MSTransitionEnd',
    'transition' : 'transitionend'
  }

}

EffecktDemos.init();
```

這 library 也是用 jQuery
所以載入順序

1. jQuery
2. Modernizer
3. CSS3-event

### list

```html
<ul class="effeckt-list" data-effeckt-type="pop-in">
    <li>list</li>
    <li class="new-item">new list</li>
    <li class="remove-item">remove list</li>
</ul>

<!-- data-effect-type 放入要呈現的動畫效果
     new-item 入場
     remove-item 退場 -->
```
