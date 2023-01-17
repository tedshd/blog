---
title: "App store & Google Play IAP((In-App Purchase)) 內購與訂閱注意事項"
date: 2023-01-12T14:51:11+08:00
draft: false
categories: [iap, google play, app store]
---

## 前期比較花時間的準備

收款銀行帳戶

公司登記資料

## 是否需要試用期

## 不同地區設定不同價格

避開匯率的問題

## 退款處理

由於是可以在商店平台做退款(所以需要客戶端或是服務端定期確認商店的訂閱狀態)

https://support.apple.com/en-us/HT204084

https://support.google.com/googleplay/answer/2479637

## 取消續訂處理

取消續訂也是需要服務端或是客戶端確認訂閱狀態

https://support.apple.com/en-us/HT202039

https://support.google.com/googleplay/answer/7018481

## 取消訂閱流程

提供商店的 support 網址

https://support.apple.com/en-us/HT202039

https://support.google.com/googleplay/answer/7018481

## 價格對應的訂閱 id 需要有後端配置下發給客戶端以利於價格調整

避免用戶使用舊版 app 訂閱舊價格

## 訂閱量與續訂的數據埋點(取消訂閱也需要上報)

須注意訂閱量與預估收入的計算

## 購買 / 訂閱狀態是跟著 Google 或是 Apple 帳號

需要注意自己服務如何和 Google 帳號或是 Apple 帳號關聯(或是訂單 id 關聯)

## 客戶端需要和商店確認訂單與後端確認訂閱狀態(增強安全性)

## App store 文案需要添加訂閱相關事項與協議

[Guideline 3.1.2 - Business - Payments - Subscriptions](https://developer.apple.com/forums/thread/112963)

這部分可以參考其他有訂閱或購買制的 App 的 App store 頁面

## iOS 需要添加恢復訂閱功能

因為服務和訂閱並非緊密關聯, 所以需要實作恢復訂閱來讓服務的帳號和訂閱能重新關聯起來