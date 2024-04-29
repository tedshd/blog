---
title: "使用 golang migrate 安裝紀錄"
date: 2024-04-29T11:15:52+08:00
draft: false
categories: [golang, migrate]
---

## Intro

在使用 golang 的情境下, 有一個很常用的 migration 工具 [golang-migrate](https://github.com/golang-migrate/migrate)

但是在不同系統下安裝我覺得不太容易

所以記錄一下

## Install

github 上有提供不同作業系統的安裝方式

[cmd/migrate](https://github.com/golang-migrate/migrate/tree/master/cmd/migrate)

目前測試 Mac / Ubuntu 有成功

1. Mac OS X

使用 homebrew 安裝

```shell
brew install golang-migrate
```

在 mac 上面安裝是蠻容易的

2. Ubuntu 20.04

在 ubuntu 遇到許多權限的問題

github 上面的 `*.deb` 安裝需要調整指令

```shell
curl -L https://packagecloud.io/golang-migrate/migrate/gpgkey | sudo apt-key add -
sudo sh -c 'echo "deb https://packagecloud.io/golang-migrate/migrate/ubuntu/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/migrate.list'
sudo apt-get update
sudo apt-get install -y migrate
```

## Usage

要連接的 DB 的格式

下面是使用 mysql

`mysql://帳號:密碼@tcp(主機位置:PORT)/DB名稱?charset=utf8mb4&loc=UTC&parseTime=True`

```shell
migrate -database 'DB_URL' -path schema/migrations up
```
