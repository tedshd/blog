---
title: "Nginx 使用 host 判斷作 reverse proxy"
date: 2022-12-02T09:54:36+08:00
draft: false
categories: [nginx]
---

直接上設定

```Nginx
server {
  listen 80;
  listen [::]:80;
  server_name api.example.com, example.com;
  location / {
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-NginX-Proxy true;
    set $proxy http://0.0.0.0:3000;
    if ($host ~ api.example.com) {
      set $proxy http://0.0.0.0:8000;
    }
    proxy_pass $proxy;
  }
}
```