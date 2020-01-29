---
layout: post
title: 'nginx - study log'
date: 2015-09-30
comments: true
categories: [nginx]
---
## nginx - Study Log

半調子的紀錄...

### Command Line

```shell

sudo service nginx start

sudo service nginx restart

sudo service nginx stop

# 測試 nginx 設定
sudo nginx -t
```

### config

```shell

# document root
root /usr/share/nginx/html;

# set page show
index index.html index.htm index.php;

# 把 lib 目錄打開
location /lib {
    autoindex on;
}

```

[refer - Can I hide all server / os info?](http://serverfault.com/questions/214242/can-i-hide-all-server-os-info)
