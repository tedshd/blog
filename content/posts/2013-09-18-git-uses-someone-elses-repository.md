---
layout: post
title: 'Git - 使用別人的 repository'
date: 2013-09-18
comments: true
categories: [git]
---
## Git - 使用別人的 repository

in GitHub

sample
use [javascript-htmlspecialchars](https://github.com/tedshd/javascript-htmlspecialchars)
use SSH
```
git clone git@github.com:tedshd/javascript-htmlspecialchars.git
// use SSH
```

單純的 clone 別人的 repository 只是只能使用它
如 commit 之後是無法 push 上去, 因為不是這 repository 的擁有者
只要進去該 repository 的 ```.git/config```
只要看見
```
[remote "origin"]
        url = git@github.com:tedshd/javascript-htmlspecialchars.git
```
url 中 ```git@github.com:``` 之後不是自己的 GitHub 帳號就代表是無法 push 的
就算在這改成自己的 GitHub 帳號也是無用的
因為沒有該 repository 在自己的 repositories 中

### 把別人的 repository 改成自己用的

1. fork 一份到自己的 GitHub
2. 從自己的 repositories git clone fork 來的 repository
3. 之後 commit 就可以 push 到自己 fork 的 repository
