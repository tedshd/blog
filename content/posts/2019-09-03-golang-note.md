---
layout: post
title: 'golang - note'
date: 2019-09-03
comments: true
categories: [golang]
---
## golang - note log

### 時間格式的雷

**2006-01-02 15:04:05**

https://golang.org/pkg/time/#Time.Format

[Golang 时间格式化的奇怪设定 —— 为什么你一直出错](https://segmentfault.com/a/1190000004222341)

### Array

[Array](https://hsinyu.gitbooks.io/golang_note/content/array.html)

### 確認 type

```golang
import "reflect"

x := 7

reflect.TypeOf(x).Kind();
```

### Convert interface to string

```golang
var x interface{} = "abc"
str := fmt.Sprintf("%v", x)
```

### Print statuct

```golang
fmt.Printf("%+v\n", struct)
```
