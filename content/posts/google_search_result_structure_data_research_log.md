---
title: "Google search result with structured data"
date: 2020-05-04T13:53:19+08:00
draft: true
---

## 前言

現在可以確認的是 Google 並不會以單純的 Google structured data 來呈現在 search result

以往驗證過的是 search result 裡的 title 和描述並不完全會採用 meta 中的 title 和 description

現在在線上的頁面也再次驗證了 Google 已經在使用 NLP 分析網站的內容了

以往是用 landing page 來測試, 因為內容不豐富所以不好測試

稍微變動 Google search result 也很難得到期望的結果

這已經和 2018 年以前的情況不一樣了

## 測試結果

[https://blog.photogrid.app/posts/how_to_add_customized_watermark/](https://blog.photogrid.app/posts/how_to_add_customized_watermark/)

[結構化測試工具](https://search.google.com/structured-data/testing-tool/u/0/?hl=zh-TW#url=https%3A%2F%2Fblog.photogrid.app%2Fposts%2Fhow_to_add_customized_watermark%2F)

![screenshot image](/images/螢幕快照_2020-05-04_下午1.49.49.png)

從上面的結果可以知道

mobile search result 的 image 是抓到頁面中的 image 而非 structure data(json-ld) 中的 image

而且 image 的 alt 也是 Google 自己判斷添加的

## 結語

有趣的一件事情是該頁面也是沒什麼內容的(因為就是個嵌入 Youtube 影片的頁面

因為這頁面最近在自然搜尋流量增加(在 Google search console 看到的)

所以就關注了一下

個人覺得這也間接驗證了兩件事

1. Google 越來越重視內容且會分析頁面的內容

2. 自然搜尋進去的點擊增加是會增加排名的, 就算沒有啥內容 XD(但是這個還要多一點驗證

所以在做頁面時也請產品或 PM 想好是要有什麼內容

給人看的懂也要給 Google 爬蟲看的懂 XD
