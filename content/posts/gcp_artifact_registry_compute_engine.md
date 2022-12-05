---
title: "Google Cloud 使用 artifact registry 和 compute engine"
date: 2022-12-01T09:58:14+08:00
draft: false
categories: [gcp,artifact registry, compute engine]
---

## 前言

基於公司之前的架構設計

使用 GCP 重現一個簡化版的部署架構

基本是使用 artifact registry 和 compute engine

GCP 官方也有 artifact registry + compute engine 的部署設計

但是因為是 side project, 不想搞得太複雜, 所以沒有採用官方的方式(官方的方式再搭配其他的服務比較建議用在正式專案上面, 會是比較有彈性且可以進行高承載的設計, 不過主要還是看預算和承載量的考量)

## 架構

side project 是一個單純的 web service

目前也不考慮高流量的問題

前後端分離, 主要會有前端的服務和 api 的服務

### google cloud

* Compute Engine(1 instance)
* Cloud SQL(1 sql, 沒有開 HA, 需要注意的是有開 HA, sql 費用會是兩倍計算)
* Artifact Registry

### code

* Vue(nuxt SSR)
* CodeIgniter 4(當作 API server)

因為會有前端和後端的部分, 會有兩個 service

1. node
2. PHP

所以最簡單的方式就是兩個分開開發

因為有使用 docker

所以就把分成兩個 docker image

要部署的程式和環境都包在 docker image 裡面

這樣在 VM 裡面不用考慮環境問題, 只要跑起來 docker container 就可以了

## 開發與部署

本地開發已經是使用 ARM 架構的 mac

所以需要注意的是 build image 時會因為不同的 CPU 架構需要 build 對應架構的 docker image

還有需要注意的是程式的套件對應開發環境的版本, 基本上除非要集小化 Image, 不然會建議 docker image 使用 Linux ubuntu 來當成 base

為了方便開發, 本地直接使用 mac 自己的環境開發

另一種做法就是本地就直接啟動使用 docker container 開發, 把要開發的程式 mount 進去

開發完後就是 build docker image

上面提到做法就是把要執行的程式和環境整個打包成 docker image

這樣部署時就不會受到部署環境影響

這邊採用的 docker image 管理服務就是 [Artifact Registry](https://cloud.google.com/artifact-registry/docs/overview)

簡單的說就是一個私有的 docker hub

AWS 對應的服務是 [Elastic Container Registry](https://aws.amazon.com/tw/ecr/)

這邊會著重在 Artifact Registry 的建立與部署

## Artifact Registry

> Artifact Registry provides a single location for storing and managing your packages and Docker container images.

從上述文件的介紹其實可以知道 Artifact Registry 不只有 docker image 的管理功能

其實還包含 Java, Node.js, Python, Debian, RPM 等等的套件管理

所以有開發以上的套件又需要有個私有的 repositories 也可以用這個服務

因為這服務的文件蠻多且有點複雜

這邊會稍微整理專注在使用 docker 相關的文件出來

1. 建立 repositories

就和使用 docker hub 一樣必須要先建立 repositories 來擺放 image

可以直接參考以下文件

[Create repositories](https://cloud.google.com/artifact-registry/docs/repositories/create-repos)

這邊建議直接在 google console 的 web 介面建立比較好操作

建立 repositories 後需要注意的是能夠操作這個 repositories 的帳號

專案擁有者一定是可以操作, 如果要要建立 CI/ÇD 的話建議另外建立 service account 來賦予相關權限

有其他開發者要共同操作的話, 就去 IAM 添加並賦予相關權限

2. 開始進行 push & pull

要在本地端進行 Artifact Registry 的 docker push & pull 操作要先具備以下條件

* 要安裝 gcloud 並且登入
* 登入的帳號需要具備 Artifact Registry 權限
* 啟動 [Artifact Registry API](https://cloud.google.com/artifact-registry/docs/enable-service)
* 設定 gcloud config [Set defaults for gcloud commands](https://cloud.google.com/artifact-registry/docs/repositories/gcloud-defaults)
* docker 設定 repositories [Changes for Docker](https://cloud.google.com/artifact-registry/docs/transition/changes-docker#artifact-registry)

在 google 其他服務大多已經具備權限了(在正式專案上建議對沒有必要的權限做關閉)

可以參考 [Deploy to Google Cloud](https://cloud.google.com/artifact-registry/docs/deploy)

來確認之後要部署時可不可以直接使用

[Install the Google Cloud CLI](https://cloud.google.com/sdk/docs/install-sdk)

安裝後登入自己的帳號或登入需要使用的 service account

其實上面講了那麼多

簡單列一下要執行的指令

```shell
gcloud auth login

gcloud services enable artifactregistry.googleapis.com

gcloud config set project <PROJECT ID>

gcloud config set artifacts/location <LOCATION>

gcloud config set artifacts/repository <REPOSITORY>

gcloud artifacts packages list --repository=<PROJECT ID>

gcloud config list

gcloud services enable artifactregistry.googleapis.com

gcloud auth configure-docker <LOCATION>-docker.pkg.dev
```

這樣之後就可以開始 pull & push 了

可以看到要拉取的 path 結構大致上如下

```
us-central1-docker.pkg.dev/my-project/team1/web-app:1.0
```

基本上結構就是

`<LOCATION>-docker.pkg.dev/<PROJECT ID>/<REPOSITORY>/<IMAGE NAME>:<VERSION>`

## 補充

有時為了指令的便利性可以利用以下設定來避免需要 sudo

[Manage Docker as a non-root user](https://docs.docker.com/engine/install/linux-postinstall/)