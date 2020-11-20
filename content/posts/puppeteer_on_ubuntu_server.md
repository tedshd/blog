---
title: "Puppeteer 安裝在 ubuntu server 使用紀錄"
date: 2020-11-20T10:52:35+08:00
draft: false
categories: [puppeteer, ubuntu, gcp]
---

Puppeteer 是 Google 推出的基於 nodejs 的一套工具
可以控制 Chrome 和 Chromium
所以在爬蟲和測試等等需求都很好用

這裡記錄一下在 GCP 上面開一台 Computer Engine 後裝 Puppeteer 的紀錄

## 1. CE 開一個 instance

之前開 f1-mirco(1vCPU & 0.6G RAM)(共用核心)

這樣的等級如果只是 load 完頁面爬內容還是可以撐得住的

但是要做一些操作行為或是下滑垃取 AJAX 內容等等就不夠用了

所以就開了一台 e2-small (2vCPU & 2GB RAM)(非共用核心) 來跑

這次是裝 ubuntu 20.04 LTS

## 2. 安裝 node

先拉 node 套件庫下來

```shell
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
```

裝 nodejs

```shell
sudo apt install nodejs
```

[Refer - How to Install Node.js and npm on Ubuntu 18.04](https://linuxize.com/post/how-to-install-node-js-on-ubuntu-18.04/)

## 3. 裝要啟動 Puppeteer 和 chrome 等相關套件

```shell
sudo sudo apt update
```

```shell
sudo apt-get install ca-certificates fonts-liberation libappindicator3-1 libasound2 libatk-bridge2.0-0 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgbm1 libgcc1 libglib2.0-0 libgtk-3-0 libnspr4 libnss3 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 lsb-release wget xdg-utils
```

[refer - Troubleshooting](https://github.com/puppeteer/puppeteer/blob/main/docs/troubleshooting.md#chrome-headless-doesnt-launch-on-unix)

通常裝完 Puppeteer 沒有啟動成功大多是有套件遺漏造成啟動不了 Chrome/Chromium

## 3. 裝 Puppeteer

```shell
npm i puppeteer
```

不要裝 puppeteer-core(因為這不包含 browser), 這個東西要裝請在自己的電腦裝來玩

[Github - puppeteer](https://github.com/puppeteer/puppeteer)

## 4. 寫個 sample code 吧

```javascript
const puppeteer = require("puppeteer");

(async () => {
  const browser = await puppeteer.launch({
    args: ["--no-sandbox"],
  });
  const page = await browser.newPage();
  await page.goto("https://google.com");
  await page.screenshot({ path: "example.png" });

  await browser.close();
})();
```

記得加上 **--no-sandbox**
有時在 terminal 有問題是因為沒加這個參數(但這是個選項)

## Troubleshooting

在 Puppeteer 有個整理出來的 Troubleshooting

如果有任何狀況都可以參考該頁面

[troubleshooting](https://github.com/puppeteer/puppeteer/blob/main/docs/troubleshooting.md)

## Log

在使用時參考 `launch` 的 `arg`

使用以下的內容當參考

[List of Chromium Command Line Switches](https://peter.sh/experiments/chromium-command-line-switches/)

puppeteer 文件也是有許多 method 的使用方式

[https://pptr.dev/](https://pptr.dev/)
