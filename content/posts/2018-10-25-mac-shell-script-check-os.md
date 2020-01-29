---
layout: post
title: 'Mac - shell script check OS'
date: 2018-10-25
comments: true
categories:
---
## Mac - shell script check OS

Use shell script check Linux or Mac

```sh
#!/usr/bin/env bash

if [ `uname` == 'Linux' ];
then
    echo 'Linux'
else
    echo 'Mac'
fi
```
