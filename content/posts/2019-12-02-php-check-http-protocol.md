---
layout: post
title: 'PHP -  check HTTP protocol'
date: 2019-12-02
comments: true
categories: [php]
---
PHP -  check HTTP protocol

Use

```PHP
$protocol    = (isset($_SERVER['HTTPS']) && ($_SERVER['HTTPS'] == 'on' || $_SERVER['HTTPS'] == 1) || isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] == 'https') ? 'https' : 'http';
```
