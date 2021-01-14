---
title: "PHP - 使用 urlencode rawurlencode 的差異和使用 http_build_query"
date: 2021-01-14T17:21:53+08:00
draft: false
categories: [PHP]
---

## 最近剛好踩到個雷

就順便筆記一下

基本上在 url query string 的 value 都要做 **url encode**

所以有個要注意的幾點是

server side 收到這個 query string 丟給程式語言處理時

1. 依照用途決定是否要
