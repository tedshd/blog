---
title: "Safari 設定 100vh 還是出現卷軸(scroll bar)"
date: 2022-06-20T14:44:30+08:00
draft: false
categories: [ios, safari]
---

## 前言

最近注意到 Safari 設定 100vh

在未滿內容的情況還是出現滑動的卷軸

這導致了體驗不佳

研究了一下發現是因為在 Safari 上有 url bar 的關係(iOS 15 以下還有 function bar)

100vh 的大小其實是這些 bar 隱藏時的大小(iOS Safari 滑動時這些 bar 會隱藏起來)

這邊試了幾種方式

## 改成 `100%`

可以改成用 100% 來取代 100vh

不過這得依情況來使用

## 使用 `-webkit-fill-available`

`-webkit-fill-available` 目前只有 iOS 支援

所以可以用 useragent 來處理樣式來對應使用這個 CSS 屬性

[範例](https://tedshd.io/demo/ui/ios_full_view.html)

## 結論

我自己測試了一下會偏好使用 `100%`

個人會希望能夠簡單處理方式就用簡單的方式處理