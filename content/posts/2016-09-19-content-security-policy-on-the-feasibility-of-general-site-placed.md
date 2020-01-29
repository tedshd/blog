---
layout: post
title: 'Content Security Policy - 論一般網站放置的可行性'
date: 2016-09-19
comments: true
categories: [CSP Security]
---
## Content Security Policy - 論一般網站放置的可行性

### 前言

Content Security Policy 出來也有一段時間了

他的目的是為了從 `header` 下手去抵禦一些攻擊, 基本上遵循它的rule 就可以避掉一些 XSS 攻擊

但有時加入這功能會需要變動程式的架構或者某些性質的服務是根本就是設定到可以動的話安全係數會降低許多

這裏會稍微舉一些例子來說明

關於 Content Security Policy 以下有一些連結可以幫助瞭解這個 header

[Refer - An Introduction to Content Security Policy](http://www.html5rocks.com/en/tutorials/security/content-security-policy/)

[Refer - Content Security Policy 入门教程](http://www.ruanyifeng.com/blog/2016/09/csp.html)

[Refer - Content-Security-Policy - HTTP Headers 的資安議題 (2)](http://devco.re/blog/2014/04/08/security-issues-of-http-headers-2-content-security-policy/)

[Refer - Content Security Policy Reference](https://content-security-policy.com/)

目前有只用的知名服務有 **github** 和 **dropbox**

### 簡介

簡單說就是會限制頁面上出現的東西
* domain
* inline style
* inline script
* iframe, frame
* object
* https

可以用 html `<meta>` 或用 http header 的方式使用, 所以純靜態網頁也是可以用的

但有個限制是用 `<meta>` 的方式就不能用 `frame-ancestors` 了

還有需注意的是 `<body onload="console.log('load')"></div>` 或 `<a href="javascript:void(0);"></a>` 這種也是 inline script

但 `a` 的例子可以在 `click` 時用 `e.preventDefault();` 避掉

這裏會著重在 iframe 的限制, 因為其他的部分上面參考文章都有詳細的說明, 但關於 iframe 卻沒有較詳細的說明

且發現在實作上跟限制 iframe 有關的設定, 在不同 browser 也有差, 甚至與 [Content Security Policy Reference](https://content-security-policy.com/) 都還有差異

以下是用 chrome 52, safari 9.1.3, firefox 48.0.2 測試的結果

1. `frame-src` 雖然被捨棄建議用 `child-src` 但 safari 不支援, 所以還是得用(把他跟 child-src 設定一樣即可)

2. `frame-ancestors` 還沒支援很多 browser, 建議還是加上 `X-Frame-Options` 的方式來達到兼容([什麼是 X-Frame-Options?](https://developer.mozilla.org/zh-TW/docs/HTTP/X-Frame-Options))

3. 每個頁面是吃該頁面的 header 的 CSP 設定, 所以 iframe 是吃 iframe 自己 header 的設定

4. 基本上放 Google 廣告聯播網的要另外處理因為程式碼如下圖, 但可以把它放到 iframe 隔離獨自處理(~~但曝光和點擊需測試一下~~ 經測試是有計算到的

<img src="https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202016-09-20%20%E4%B8%8A%E5%8D%8810.51.07.png?alt=media&token=6b99ed0c-c6fe-45de-9455-85f9a0f69391" width="80%" style="display:inline-block;margin:0 auto;">

以下是範例可以玩玩看

[github demo code](https://github.com/tedshd/content-security-policy-example)

最後可能有人有疑問那用 browser 的 devtool 去操作 js 改動頁面或執行 js, CSP 可以擋得住嗎?

擋不住啊, 因為 CSP 是 header, 它在 response 時檢查 header 去了解之後進來的 content 必須符合 CSP 的設定, 不然就擋掉 ,當然沒辦法管已經載完的頁面你要怎麼用 devtool 玩頁面都無法阻擋

