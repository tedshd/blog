---
title: "docker 使用紀錄"
date: 2020-12-24T10:12:17+08:00
draft: false
categories: [docker, mac]
---

## `docker images`

列出所有拉下來的 docker image

```shell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
ubuntu              latest              07f8e8c5e660        3 weeks ago         188.3 MB
```

## build dockerfile

使用 dockerfile 建立 docker image

直接建立

```shell
docker build .
```

預設會找當前的目錄的 `Dockerfile`

`-t` 可以設定建立的 image & tag name

```shell
docker build . -t image_name:tag_name
```

`-f` 指定用哪個 dockerfile 建立

```shell
docker build . -t ubuntu_dev:16.04 -f local.Dockerfile
```

## dockerfile 使用

### 使用 nginx official image 建立

```dockerfile
FROM nginx:1.19.6-alpine

COPY ~/www /usr/share/nginx/html

EXPOSE 80
```

### multi stage 多次 build image

有時最終要包起來的 image 會做多次處理

兩種做法

1. 要多次處理的部份

依照要處理的部份個別建立 docker 處理

最後在把要包起來的東西包成 docker

2. 用 multi stage

```dockerfile
FROM golang:1.7.3 AS builder
WORKDIR /go/src/github.com/alexellis/href-counter/
RUN go get -d -v golang.org/x/net/html
COPY app.go    .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /go/src/github.com/alexellis/href-counter/app .
CMD ["./app"]
```

都是放在一起 build, build 完之後可以把結果複製到會後再使用的 image 裡面

多用於要先編譯的情況

先在其他 image 編譯完

最後在把執行環境包成 image

[Refer](https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds)

但是 build 完之後會有個問題, 就是之前 stage build 出來的 image 基本上沒有必要保留

所以可以用 `docker image prune f` 移除掉之前 stage 建立的 image

[Refer - How to remove intermediate images from a build after the build?](https://stackoverflow.com/questions/50126741/how-to-remove-intermediate-images-from-a-build-after-the-build)

[Refer - Prune unused Docker objects](https://docs.docker.com/config/pruning/)

## 建立 container `docker run`

`docker run -t -i ubuntu /bin/bash`

```shell
docker run -t -i ubuntu /bin/bash
root@b0cdeb409841:/#
```

建立 container 並執行 bash

### docker run

```shell
docker run -idt --name <container name> -v <mount absolute path or ~ path>:<docker path> <IMAGE>:<TAG>
```

## `docker ps -a`

列出所有已經建立的 container

## `docker ps`

列出所有正在執行的 container

## `docker start <container_id>`

執行 container

## `docker stop <container_id>`

停止 container

## `docker logs <container_id>`

查看 docker 處理的紀錄
