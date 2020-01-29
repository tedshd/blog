---
layout: post
title: 'JavaScript - 使用與處理正確的時間'
date: 2018-09-20
comments: true
categories:
---
## JavaScript - 使用與處理正確的時間

這是個很有趣的議題

舉凡使用倒數計時器或限時開賣等

只要在網頁上牽扯到時間的動態呈現都需要處理這問題

會列舉了幾個情況與介紹一些跟時間相關的的概念與 API

[Refer - 深入理解定时器系列第一篇——理解setTimeout和setInterval](https://www.cnblogs.com/xiaohuochai/p/5773183.html)

```JavaScript
var options = {
    timeZone: 'Europe/London',
    year: 'numeric', month: 'numeric', day: 'numeric',
    hour: 'numeric', minute: 'numeric', second: 'numeric',
};
formatter = new Intl.DateTimeFormat([], options);
formatter.format(new Date());

```

[Refer - Get time of specific timezone [duplicate]
](https://stackoverflow.com/questions/8207655/get-time-of-specific-timezone)

[Refer - Getting To Know The JavaScript Internationalization API](https://netbasal.com/getting-to-know-the-javascript-internationalization-api-cb893b3908e0)

[Refer - Javascript 的 EventLoop](https://github.com/HXWfromDJTU/blog/blob/master/JS/eventloop.md)
