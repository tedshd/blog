---
layout: post
title: 'JavaScript - Scroll Progress'
date: 2014-03-02
comments: true
categories: [JavaSript]
---
## JavaScript - Scroll Progress

Show a progress bar about page scroll position.

This used scroll event
Progress bar must handle scroll position and scroll total height, and show it for percent
View MDN document can find it can't use `scrollHeight`, because when scroll bar scroll to bottom, `scrollTop` not equal `scrollHeight`

```javascript
dom = document.querySelector('body');
percent = (dom.scrollTop/(dom.scrollHeight - document.documentElement.clientHeight))*100 + '%';
```

Then find `scrollTop` didn't work in firefox

```javascript
if (dom.scrollTop) {
	percent = (dom.scrollTop/(dom.scrollHeight - document.documentElement.clientHeight))*100 + '%';
} else {
	percent = (window.pageYOffset/(dom.scrollHeight - document.documentElement.clientHeight))*100 + '%';
}
```

[GitHub](https://github.com/tedshd/scroll_progress)


[Refer - onscroll event | scroll event](http://help.dottoro.com/ljurkcpe.php)
[Refer - Element.scrollTop - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element.scrollTop)
[Refer - element.scrollHeight - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element.scrollHeight)
[Refer - retrieve Scrollbar position with javascript](http://stackoverflow.com/questions/2481350/retrieve-scrollbar-position-with-javascript)
