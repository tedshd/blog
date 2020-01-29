---
layout: post
title: 'HTML5 - Full Screen Mode'
date: 2014-05-08
comments: true
categories: [HTML5, javascript, google]
---
## HTML5 - Full Screen Mode

It can control full screen the browser
IE if it is to be more than IE11

### Code

```javascript
function toggleFullScreen() {
  if (!document.fullscreenElement &&    // alternative standard method
      !document.mozFullScreenElement && !document.webkitFullscreenElement && !document.msFullscreenElement ) {  // current working methods
    if (document.documentElement.requestFullscreen) {
      document.documentElement.requestFullscreen();
    } else if (document.documentElement.msRequestFullscreen) {
      document.documentElement.msRequestFullscreen();
    } else if (document.documentElement.mozRequestFullScreen) {
      document.documentElement.mozRequestFullScreen();
    } else if (document.documentElement.webkitRequestFullscreen) {
      document.documentElement.webkitRequestFullscreen(Element.ALLOW_KEYBOARD_INPUT);
    }
  } else {
    if (document.exitFullscreen) {
      document.exitFullscreen();
    } else if (document.msExitFullscreen) {
      document.msExitFullscreen();
    } else if (document.mozCancelFullScreen) {
      document.mozCancelFullScreen();
    } else if (document.webkitExitFullscreen) {
      document.webkitExitFullscreen();
    }
  }
}
```

### Example

HTML

```html
<button id="full">Full Screen</button>
```

JavaScript

```javascript

document.querySelector('#full').addEventListener('click', function() {
    toggleFullScreen();
});

function toggleFullScreen() {
  if (!document.fullscreenElement &&    // alternative standard method
      !document.mozFullScreenElement && !document.webkitFullscreenElement && !document.msFullscreenElement ) {  // current working methods
    if (document.documentElement.requestFullscreen) {
      document.documentElement.requestFullscreen();
    } else if (document.documentElement.msRequestFullscreen) {
      document.documentElement.msRequestFullscreen();
    } else if (document.documentElement.mozRequestFullScreen) {
      document.documentElement.mozRequestFullScreen();
    } else if (document.documentElement.webkitRequestFullscreen) {
      document.documentElement.webkitRequestFullscreen(Element.ALLOW_KEYBOARD_INPUT);
    }
  } else {
    if (document.exitFullscreen) {
      document.exitFullscreen();
    } else if (document.msExitFullscreen) {
      document.msExitFullscreen();
    } else if (document.mozCancelFullScreen) {
      document.mozCancelFullScreen();
    } else if (document.webkitExitFullscreen) {
      document.webkitExitFullscreen();
    }
  }
}
```

### CodePen

<p data-height="268" data-theme-id="2982" data-slug-hash="ExLCA" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/tedshd/pen/ExLCA/'>full screen mode</a> by Ted (<a href='http://codepen.io/tedshd'>@tedshd</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

### Other use

Use it make youtube api player full screen
If render player on `<div id="player"></div>`

```javascript

document.querySelector('#full').addEventListener('click', function () {
  toggleFullScreen(document.querySelector('#player'));
});

function toggleFullScreen(el) {
  if (!document.fullscreenElement &&    // alternative standard method
      !document.mozFullScreenElement && !document.webkitFullscreenElement && !document.msFullscreenElement ) {  // current working methods
    if (document.documentElement.requestFullscreen) {
      el.requestFullscreen();
    } else if (document.documentElement.msRequestFullscreen) {
      el.msRequestFullscreen();
    } else if (document.documentElement.mozRequestFullScreen) {
      el.mozRequestFullScreen();
    } else if (document.documentElement.webkitRequestFullscreen) {
      el.webkitRequestFullscreen(Element.ALLOW_KEYBOARD_INPUT);
    }
  } else {
    if (document.exitFullscreen) {
      document.exitFullscreen();
    } else if (document.msExitFullscreen) {
      document.msExitFullscreen();
    } else if (document.mozCancelFullScreen) {
      document.mozCancelFullScreen();
    } else if (document.webkitExitFullscreen) {
      document.webkitExitFullscreen();
    }
  }
}
```

[Refer - Using fullscreen mode - Web developer guide | MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Using_full_screen_mode)

[Refer - 全螢幕 API (Windows)](http://msdn.microsoft.com/zh-tw/library/ie/dn265028(v=vs.85).aspx)

[Refer - How to Use the HTML5 Full-Screen API (Again) - SitePoint](http://www.sitepoint.com/use-html5-full-screen-api/)
