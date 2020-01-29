---
layout: post
title: 'Web - viewport 是啥?你真的了解移動裝置的畫面大小處理嗎?來講古了'
date: 2018-08-23
comments: true
categories:
---
## Web - viewport 是啥?你真的了解移動裝置的畫面大小處理嗎?來講古了

### 歷史

早期 viewport 是可以設定跟 device 的 dpi 一樣的(target-densitydpi=device-dpi), 但這時就有個問題就是當 viewport 的這個設定沒設定時, browser 上顯示的寬高就會不一樣了, 再者早期 mobile device 剛邁入 high resolution 的顯示就會顯得亂七八糟, Apple 是最早意識到這點, 所以它也是最早處理這個問題的, 就是直接在 OS 與 browser 上處理分辨率的問題, 不直接採用實際上螢幕 high resolution 的大小.

這也是為啥 Macbook pro 明明是 2K 螢幕但是 browser 的 px 只有 1280x720 左右, 那這又延伸另一個問題把分辨率變大就照成圖片等非向量顯示的圖片會失真, 所以就是為啥有 media query(device-pixel-ratio) or (min-resolution) 抑或 img srcset 等屬性的出現, 就是為了處理 high resolution 時圖片變糊的問題.

在 2018 年的現在 mobile device 的 browser 解析度都不會是真實 device 的解析度了, 已經在 OS 抑或 browser 處理掉了

### 解決方案

請讓 layout 儘量是彈性布局, RWD 不是讓你處理不同 device 的問題, 是讓你處理畫面大小與 high resolution 與螢幕方向的方式

網頁的 UI 不像一現實上的平面視覺大小是死的(很多剛進入業界的設計師都會遇到這問題, 甚至 F2E 也是如此)

client 端有很多的畫面大小, 所以必須讓你的 layout 設計是有彈性可以符合在不同畫面大小上的呈現, 如果 Layout 或 UI 太複雜, 那就得考慮 AWD 的設計

AWD(Adaptive Web Design) 是以 server side 辨別 UserAgent 來決定 client 需要呈現的元件

好處顯而易見的就是可以依照 UA(UserAgent) 決定要到 client 的 UI 元件再搭配 RWD 可以真正的做到靈活的彈性配置


[Refer - 在移动浏览器中使用viewport元标签控制布局](https://developer.mozilla.org/zh-CN/docs/Mobile/Viewport_meta_tag)

[Refer - Configuring the Viewport](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html)
