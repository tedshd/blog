---
layout: post
title: 'JavaScript - touch and click behavior in mobile browser'
date: 2016-09-07
comments: true
categories: [JavaScript]
---
## JavaScript - touch and click behavior in mobile browser

On mobile web

If you click it

And mobile browser can fire `touchstart` and `click`

Fire `touchstart` event and then fire `click` event has the difference in time.

the step is `touchstart -> click`

So if you has a popup and you use `touchstart` event bind close behavior.

You can find it fire click event.

Then some bug happened.

In this case(suggest use mobile browser)

https://tedshd.io/demo/touch_test.html

When you click close.

Then popup closed.

Because the difference in time.

Then `click` event fired the popup is closed.

So `click` event can click a link.

Because the `click` event is click that position and that position has a link.

So it can click a link.

### Solution

1. Use `click` bind.

2. Use `e.preventDefault()` in `touchstart` event, but it also can stop fire `touchmove` and `touchend` event.

[Reference - Ghost clicks in mobile browsers](http://ariatemplates.com/blog/2014/05/ghost-clicks-in-mobile-browsers/)
