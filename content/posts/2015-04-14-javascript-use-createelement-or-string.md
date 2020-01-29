---
layout: post
title: 'JavaScript - Use createElement or string?'
date: 2015-04-14
comments: true
categories: [JavScript]
---
## JavaScript - Use createElement or string?

常常討論在頁面上塞入新的 DOM 究竟是用哪種方式好

其實在現今是要看 browser 如何解析 JavaScript

所以目前沒一定的答案

以下為效能測試的數據

[jsperf - dom-test-string-vs-createelement](http://jsperf.com/dom-test-string-vs-createelement)

雖然樣本數少

但依據上面的結果用 `createElement` 還是較有優勢
