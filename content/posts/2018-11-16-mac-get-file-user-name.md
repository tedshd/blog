---
layout: post
title: 'Mac - Get file user(owner) name & user id'
date: 2018-11-16
comments: true
categories: [Mac]
---
## Mac - Get file user name & user id

### Get file owner name

```shell
stat -f '%Su' <file or folder name>
```

### Get user id

#### show user

```shell
id
// or
id <user name>
```

#### get uid

```
id -u
// or
id -u <user name>
```

### get file owner uid

~~stat -f '%Su' `<file or folder name>` | xargs id -u~~

```
stat -f '%u' <file or folder name>
```

[Refer - 将Linux命令的结果作为下一个命令的参数](https://my.oschina.net/leopardsaga/blog/112335)
