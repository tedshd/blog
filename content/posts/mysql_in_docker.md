---
title: "Mac M1 run MySQL in local docker"
date: 2022-05-03T15:53:18+08:00
draft: false
categories: [docker, mysql]
---

## Usage

[docker hub](https://hub.docker.com/_/mysql)

In Apple M1

[amd64/mysql](https://hub.docker.com/r/amd64/mysql/)

## Run docker in local

Sample for M1(different of image name)

```shell
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password -d amd64/mysql:latest
```

Container run in `0.0.0.0`

```shell
mysql --default-character-set=utf8mb4 -u root -h 0.0.0.0 -P 3306 -p -A
```