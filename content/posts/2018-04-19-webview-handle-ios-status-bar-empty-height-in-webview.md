---
layout: post
title: 'webview - handle iOS status bar empty height in webview'
date: 2018-04-19
comments: true
categories: [webview]
---
## webview - handle iOS status bar empty height in webview

in iOS

If you use fullscreen webview in app and set app size over iOS device navigation bar.

So need add height to fill status bar height.

iPhone6/7/8 is `20px`

iPhoneX is `44px`

You can use is sample code

```javascript
header.ios {
    padding-top: 20px;
}
@media (width: 375px) and (height: 832px)  {
    header.ios {
        padding-top: 44px;
    }
}
```

iPhoneX fullscreen webview width is `375px`, height is `832px`
