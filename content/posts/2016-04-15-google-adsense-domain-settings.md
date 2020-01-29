---
layout: post
title: 'Google Adsense domain 設置'
date: 2016-04-15
comments: true
categories: [Google, ad]
---
## Google Adsense domain 設置

一點設定 Google adsense 的心得

因為有時會寫一寫筆記或部落格記錄人生

然後因為工作進到跟廣告有點關係的公司, 遇到裡面的一些專家

有人提議說, 既然我有寫文章的習慣, 那也可以放個廣告賺一點錢

但我個人是不太喜歡放廣告, 畢竟大家都知道廣告是拖累網站速度的元凶

但最近想說試試可不可以在自己的網站放個一個版位的廣告, 看能不能抵掉 GCP 維持的費用(應該是不太可能...

所以就在自己寫的 blog 和自己做的一些 service 放上去試試

這紀錄一下一些在用 Google adsense 比較特別的行為與情況

### US 100 才能領出來

我這要等到幾時啊...

### Google adsense 是動態 CPC + CPM 計算價錢

所以沒一定的價格, 似乎有受流量影響

### 眾所皆知, 廣告通常是 by domain 申請, 現在用 subdomain 是不行的

很久以前依據在 subdomain service 的話似乎可以, 但現在不行了

因為我用 logdown 申請說不能用 subdomain 申請...(明明約半年前還可以, 只是當時不知為何一直說我違反他們的協議, 所以一直申請不過

但 Google 自己的 blogger 卻可以, 我試過了因為我有個 blogger, 但 Pixnet 我沒試過(不過 Pixnet 可以跟他們自己申請廣告分潤

### Google Adsense 的網站審查蠻嚴謹的

嚴謹到我這 logdown 之前都過不了(靠, 搞得我都認為是 XXX 的錯...

### 把自己的站用 submain 掛到申請過 doamin 下去可行

我本身是這樣試出來可以的

### How to do?

我申請 tedshd.io 放 Google adsense

在 tedshd.io 開個 subdomain blog.tedshd.io

設定 blog.tedshd.io CNAME	tedshd.logdown.com

這樣 blog.tedshd.io 就是 tedshd.logdown.com

這樣 Google adsense 就會有了

且去 Google adsense 後台看也有數據進來了

但這不知道是漏洞還是 Google 有意為之

個人覺得這算黑的做法

所以哪天被鎖就 GG 了...
