---
title: "修復 mac m1 開機偵測不到 type-c 螢幕"
date: 2023-01-08T14:40:14+08:00
draft: false
categories: [mac]
---

最近突然發現 mac 在重開機或是關閉後開機時

type-c 的螢幕無法被偵測到

拔插 type-c 和 mac 那端的連接也沒用

得拔插螢幕端的 type-c

就覺得很奇怪, 因為之前都是正常的

所以先推測是 mac OS 的版本問題

從 12.x -> 13.1 後發現還是一樣...

所以就認真在網路找了一下有沒有人碰過這樣的問題

先找到一個類似的

但是裡面說 12.x 後修復的問題

所以我推測應該是別的問題

就繼續找

最後找的了這篇文章

[17 Ways To Fix External Monitors Not Working On Mac (inc. M1/ M2 Macs, Ventura & Monterey)](https://machow2.com/external-display-issues/)

17 種慢慢試總算可以找到原因吧

但也不是傻了從第一條開始試

所以先看了一下有哪些方法

結果就馬上喵到一個最有可能的問題

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E6%88%AA%E5%9C%96%202023-01-08%20%E4%B8%8B%E5%8D%882.36.33.png?alt=media&token=5d8791ee-7a40-4ff2-b0d6-09ba7ea1991c)

一改完就恢復正常了

內文是說到

> macOS Ventura introduced a new feature “USB Restricted Mode” for M1 and M2 Macs which requires you to allow USB-C devices such as monitors to connect to your Mac.

但奇怪的是我在 mac OS 12 就遇到這問題

所以當時就先升版本到 mac OS 13(Ventura) 才改

所以也不太肯定 mac OS 12 是不是可以用這問題解決