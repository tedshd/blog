---
layout: post
title: 'JavaScript - handle load img fail'
date: 2014-07-01
comments: true
categories: [javascript]
---
## JavaScript - handle load img fail

Sometime load image from server or other place fail(404 not found), we must prepare default image.

A simple way

```html
<img src="avatar.svg" onerror="this.src='/static/ico_default_avatar.png';this.onerror=null;">
```
