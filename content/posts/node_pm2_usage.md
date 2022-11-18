---
title: "Node PM2 使用紀錄"
date: 2022-11-18T10:47:52+08:00
draft: false
categories: [nodejs, pm2]
---

## 介紹

[PM2](https://pm2.keymetrics.io/) 是一個可以方便處理 node process 的工具

大多用於線上環境

這邊主要紀錄 PM2 的一些用法與指令

## 基本使用

可以參考官方文件 [PM2 Process Management Quick Start](https://pm2.keymetrics.io/docs/usage/quick-start/)

安裝

```shell
npm install pm2 -g
```

啟動

```shell
pm2 start <要啟動的 js>
```

通常建議啟動時的指令搭配以下參數(更多參數請詳閱文件)

```shell
# Specify an app name
--name <app_name>

# Watch and Restart app when files change
--watch

# Set memory threshold for app reload
--max-memory-restart <200MB>

# Specify log file
--log <log_path>
```

## 重新載入

```shell
pm2 reload <要重啟的 app>
```

大多用於程式部署更新後, 有較好的體驗(和 restart 相比)

可以參考以下比較

[refer - What is the difference between pm2 restart and pm2 reload](https://stackoverflow.com/questions/44883269/what-is-the-difference-between-pm2-restart-and-pm2-reload)

## log 紀錄

推薦使用 [pm2-logrotate](https://github.com/keymetrics/pm2-logrotate)

來處理 logrotate

當然如果有指定 log path 的話, 用系統處理 logrotate 也是可以的

如果要清空 log

可以使用 `pm2 flush`

## 監控

預設有兩種

1. Terminal

```shell
pm2 monit
```

就會開啟終端機的 dashboard 可以監控狀態

2. web

```shell
pm2 plus
```

或是用

[app.pm2.io](https://pm2.io/docs/plus/overview/#features-available-in-pm2-plus)

## LOAD-BALANCING

pm2 已經內建負載平衡的功能

[LOAD-BALANCING (CLUSTER MODE)](https://pm2.io/docs/runtime/guide/load-balancing/)