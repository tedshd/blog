---
title: "PWA(progressive web app) 漸進式網路應用程式 研究筆記"
date: 2025-05-05T08:32:05+08:00
draft: false
categories: [pwa, web]
---

## Intro

關於 PWA(progressive web app) [MDN](https://developer.mozilla.org/zh-TW/docs/Web/Progressive_web_apps) 已經有詳細的介紹了, 所以就不多說了

主要記錄以目前 2025 年的當下對瀏覽器的支援現況

## 系統支援度

目前在 mac chrome / Safari 和 windows chrome / Edge 都可以支援

mobile device 的話, iPhone Safari 支援, Android 大多支援, 少部分因為 OEM 品牌可能因為魔改了 Android 系統, 會導致 PWA 安裝了, 但是不會出現, 相當於沒有安裝成功

以下整成表格

| mac | windows | iOS | Android |
| --- | --- | --- | --- |
| 支援 | 支援 | 支援 | 部分手機型號不支援 |

## 不支援的解決方案

目前也嘗試不出來有其他的解決方案, 所以會建議在統一的使用體驗上不要去支援 PWA, 這樣在 mobile device 上面就只會是單純的添加捷徑的功能

## 測試

可以用以下連結測試 PWA

https://pwa2.tedshd.io/

## other

因為研究 PWA

順便讓之前自己設計的簡易框架也支援一下 PWA

https://github.com/tedshd/WebSimpleFrame
