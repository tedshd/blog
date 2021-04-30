---
title: "Nginx 使用 refer 處理 CORS header"
date: 2021-04-30T15:51:04+08:00
draft: false
categories: [nginx, cors]
---

處理 CORS 算是許多 Web 開發者會處理的情況

其中要又有一個比較重要的部分就是要設定 `Access-Control-Allow-Origin` 這個允許來源的 header

通常為了安全性問題, 都是只會設定允許的 host 上去

但是常常設定而且在不同環境設定也是有點麻煩

所以這邊就用了直接在 server 設定的方式來處理

這樣直接看 server 的 rule 設定即可

也可以快速的條列不同環境的 host

## 用法

```conf
if ($http_referer ~* example.com) {
    add_header 'Access-Control-Allow-Origin' 'https://example.com';
}

if ($http_referer ~* dev.example.com) {
    add_header 'Access-Control-Allow-Origin' 'https://dev.example.com';
}
```

這個判斷沒有固定的寫法

可以參考底下 Nginx 對 `http_referer` 的介紹來針對需要判斷 host 的方式進行修改


[Refer - 跨來源資源共用（CORS）](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/CORS)

[Refer - Module ngx_http_referer_module](http://nginx.org/en/docs/http/ngx_http_referer_module.html)
