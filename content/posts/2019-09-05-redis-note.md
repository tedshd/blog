---
layout: post
title: 'redis - note'
date: 2019-09-05
comments: true
categories: [redis]
---
## redis - note

doc

http://redisdoc.com/index.html

php redis

https://www.cnblogs.com/ikodota/archive/2012/03/05/php_redis_cn.html

go redis

https://godoc.org/github.com/go-redis/redis

### 連到 redis server

* local server

```
redis-cli
```

* remote server

```
redis-cli -h host -p port -a password
```

### Get all key

```
KEYS '*'
```

## Troubleshooting

### ERR Operation against a key holding the wrong kind of value

取 Key 的類型不對

用

```
type <KEY>
```

來確認存的類型
