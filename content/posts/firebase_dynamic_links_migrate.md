---
title: "Firebase dynamic links 遷移轉換"
date: 2024-04-11T11:28:12+08:00
draft: false
categories: [firebase]
---

## Intro

服務終有停止的一天

firebase 動態連結將於 2025 年 8 月 25 日關閉。

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/blog%2F截圖%202024-04-11%20上午11.34.10.png?alt=media&token=177c4740-af77-4b0d-8ad3-b6b85d5304f8)

所以要提前做遷移轉換或是找其他替代方案

## Firebase 建議

可以參考 Firebase 文件的建議自己搞

[從動態鏈接遷移到應用程式連結和應用程式鏈接通用連結](https://firebase.google.com/support/guides/app-links-universal-links?hl=zh-tw)

自己搞的好處是能搞成符合自己需求的東西

但是最大的麻煩點是要記錄的話就得自己搞數據

很多時候都會需要紀錄點擊轉換

這就得自己搞了

## 第三方服務

其實除了自己搞以外

還有很多第三方服務有在做這個東西

目前有找到的有

### [Branch io](https://www.branch.io/)

* https://www.branch.io/what-is-deep-linking/

branch io 還有個教學文

[How to migrate from Firebase Dynamic Links](https://www.branch.io/guides/how-to-migrate-from-firebase-dynamic-links/)

### [Appsflyer](https://www.appsflyer.com/)

* https://www.appsflyer.com/products/customer-experience-deep-linking/

### [kochava](https://www.kochava.com/)

* https://www.kochava.com/product/deep-linking/links/?int-link=menu-links

上面列出來的是比較常見的幾個

應該還有其他服務沒有列出來

這個就評估下要用哪個服務