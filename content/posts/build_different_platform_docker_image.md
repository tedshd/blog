---
title: "docker 建立不同平台的 image"
date: 2022-06-29T10:45:39+08:00
draft: false
categories: [docker]
---

## 前言

現在在開發與線上環境常常會遇到不同 CPU 架構的問題

不同 CPU 架構底層的指令集也不一樣

最常見的影響就是在其中一個平台編譯出來的程式會無法在另一個平台執行

這情況尤其是會在接近底層的程式上見到

現在普遍來說會發現在 ARM 架構底下有些程式執行起來效率更高

所以有部分公司的服務也會在線上環境的機器選用 ARM 架構的機器

## 情境

雖然以前公司的情況是開發在 x86-64 上

線上是 ARM 的情況

但現在自己在試驗的情況是反過來的 XD

現在 Macbook 是 M1 晶片了, M 系列是 ARM 架構

我在 GCP 開的機器是 x86-64 架構

所以在 Mac 上面 build 的 docker image 是沒法在 GCP 開的機器運行

只要執行 docker run 就會出現錯誤提示說架構不同無法執行

## 解決方案

docker 有提供可以建構不同平台的 image 的指令

只要多一個 `buildx` 和 `--platform` 的指令與參數

```
docker buildx build --platform=linux/amd64,linux/arm64 .
```

[Faster Multi-Platform Builds: Dockerfile Cross-Compilation Guide](https://www.docker.com/blog/faster-multi-platform-builds-dockerfile-cross-compilation-guide/)