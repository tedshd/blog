---
layout: post
title: 'Chrome headless 研究筆記'
date: 2018-12-26
comments: true
categories: [Google, headless]
---
## Chrome headless 研究筆記

最近要用到 chrome headless 的部分功能

且得在 ubuntu or debian server 實踐

所以筆記一下

### Intro

headless 大致分兩種用法

1. CLI

2. libary

[Refer - Getting Started with Headless Chrome](https://developers.google.com/web/updates/2017/04/headless-chrome)

CLI 用法簡單但是受限很多且沒有找到具體詳細完整的文件, 就連用 man 查都查不到...

也有可能是我自己沒有認真找

libary 就相對容易, 連 Google 自己都有提供部分語言的版本, 且有前端工程師很熟的 Node 版本

### on ubuntu server

```
sudo apt-get install chromium-browser
```

ex:

```
chromium-browser --headless --screenshot=test.png --disable-gpu --window-size=320,480 --user-agent="Mozilla/5.0 (iPhone; CPU iPhone OS 7_1_2 like Mac OS X) AppleWebKit/537.51.2 (KHTML, like Gecko) Version/7.0 Mobile/11D257 Safari/9537.53" http://tedshd.logdown.com
```

這指令下了截圖, 設定寬高, 模擬 UserAgent

當然也有 `--dump-dom` 可以看 source code

### 使用 puppeteer 處理

[puppeteer](https://github.com/GoogleChrome/puppeteer)

puppeteer 是 Google 維護的用 node 處理 headless 的套件

用了一下真是感到清爽好用

放一段最簡單的 smaple code

```JavaScript
const puppeteer = require('puppeteer');

(async () => {
    const browser = await puppeteer.launch();
    const page = await browser.newPage();
    page.setUserAgent('Mozilla/5.0 (Macintosh; Intel Mac OS X 10.12; rv:64.0) Gecko/20100101 Firefox/64.0');
		await page.goto('https://tysh310246.blogspot.com');

    await page.screenshot({path: 'example.png', fullPage: true});
    await browser.close();

})();
```

就是如此清爽

且有很多包好的 function 可以用

看了一下文件根本可以用 headless 取代 selenium + webdriver.io 了

但是目前的需求也不需要用到太多其他的功能

有空再慢慢研究

[Puppeteer API Tip-Of-Tree](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md)

### 字型

在一台 server 上除非要截的網站是用 webfont 不然就會發現截的圖因為沒有字型所以中文會是方塊字

這部分就得處理一下

可以直接裝 Google 的 noto 字型

```
wget -c https://noto-website.storage.googleapis.com/pkgs/Noto-hinted.zip
```

把字型檔載下來放在

```
/usr/local/share/fonts/
```

設定 owner

設定權限

安裝字型

```
sudo fc-cache -fv
```

搞定

這邊建議直接裝全部語系的字型較為完整, 以免會遇到其他語系還是會有問題

[Refer - Ubuntu環境下，手動安裝思源字型](http://samwhelp.github.io/blog/read/linux/ubuntu/font/font-noto/)
