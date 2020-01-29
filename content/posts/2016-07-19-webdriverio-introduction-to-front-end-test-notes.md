---
layout: post
title: 'webdriver.io - 前端測試入門筆記...'
date: 2016-07-19
comments: true
categories: [webdriver BDD]
---
## webdriver.io - 前端測試入門筆記...

前端測試工具很多種

我這裡的需求是要做自動化測試

不知為何就選了這套 [webdriver.io](http://webdriver.io/)

可能就只是單純名字很炫(誤

當然一開始要先要有 [Selenium](http://www.seleniumhq.org/)

但為何 Selenium 跟我以前的印象有差別了...

我發現它的 firefox add-on 不能把錄製的動作輸出成 code 了, 是我的錯覺嗎?還是改方式了

但我想說就算了, 直接用寫的也罷

webdriver.io 只是因為是在我看過的關於測試文章中最後有印象的東西所以就去找它了(這是事實...

也還好我的記憶沒錯, 看了介紹和文件覺得 webdriver.io 有符合我的需求且又是用 Node.js 來寫, 所以對我較友善

先記錄一下使用流程

### Base tool

* Java

```shell
sudo apt-get update

java -version

sudo apt-get install default-jre

sudo apt-get install default-jdk
```

* Node.js

[Install](https://nodejs.org/en/download/package-manager/)

### On Local

[Get Started](http://webdriver.io/guide.html)

突然發現文件寫得很詳細了...

雖然在做設定那有些選項不同但也影響不大

但想玩進階的方式可參考以下文章

[設定 Selenium 參數可參考](https://siteobservers.zendesk.com/hc/en-us/articles/201989070-Start-selenium-server-with-additional-command-line-arguments)

基本上以下是我建的順序

#### 1 先建 `package.json`

```javascript
{
  "name": "webdriver",
  "description": "automation test",
  "devDependencies": {
  }
}
```

#### 2 下載 Selenium server

之後有新版請再去確認版本

```shell
curl -O http://selenium-release.storage.googleapis.com/2.53/selenium-server-standalone-2.53.0.jar
```

#### 3 裝 webdriver

```shell
npm install webdriverio --save-dev
```

#### 4 安裝各個 OS 對應的 webdriver

[selenium-webdriver](https://www.npmjs.com/package/selenium-webdriver)

可以不必裝 `selenium-webdriver`

只要去下載各個 OS 對應要用的 browser 的 webdriver 放在專案資料夾就好了

#### 5 這樣就好了

#### 6 啟動 Selenium server 並開始寫一個簡單的自動化測試的 test case

```shell
java -jar selenium-server-standalone-2.53.0.jar
```

`test.js`

```JavaScript
var webdriverio = require('webdriverio');
var options = {
    desiredCapabilities: {
        browserName: 'firefox'
    }
};

webdriverio
    .remote(options)
    .init()
    .url('http://www.google.com')
    .getTitle().then(function(title) {
        console.log('Title was: ' + title);
    })
    .end();
```

```shell
node test.js
// output Title was: Google
```

這時你就會發現你的 firefox 被打開連到 Google 後就自動關掉

然後 terminal 就會 output `Title was: Google`

關於測試的的 script 攥寫請參考 API 文件

[WebdriverIO - API Docs](http://webdriver.io/api.html)

我預設使用 [mocha](https://mochajs.org/)

有用 [chai](http://chaijs.com/) 加強攥寫 script

### 進階應用

基本上 webdriver 分兩種測試方式

1. Standalone Mode

2. The WDIO Testrunner

各有優缺點, 就看習慣用哪種方式來跑測試

我較喜歡用 The WDIO 的方式, 因為他是把設定檔抽出來, 較好管理且可用 hook 做其他事情

依我所做的較特別的設定就是把 test case 切很細(因為測試的 scope 需求), 這就需要設定能跑個別的測試

就需要在 config 設定 `suites`

就可以這樣下 command

```shell
./node_modules/.bin/wdio wdio.conf.js --suite test_a
// or
./node_modules/.bin/wdio wdio.conf.js --suite test_b
```

可參考以下文件

[WebdriverIO - Configuration](http://webdriver.io/guide/getstarted/configuration.html)

[WebdriverIO - Test Runner](http://webdriver.io/guide/testrunner/gettingstarted.html)

一般都會要把測試結果 output 出來, webdriver 提供自訂 reporter 的功能

就看個人喜好選擇

[WebdriverIO - Dot Reporter](http://webdriver.io/guide/reporters/dot.html)

但我這需求簡單且需要讓其他人可在測試當下就輕易看到結果, 所以就在 config 設定 hook

讓測試跑完時儲存測試結果並有個頁面讓別人看

config 的 hook

```JavaScript
afterTest: function (test) {
    console.log('HOOK - afterTest:', test);
},
```

test 就是測試結果

hook 也有很多狀態可用

### <strong style="color:red">廢棄方法(因為一直試驗失敗...</strong>

### On remote Server

基本上用 webdriver 做測試是需要有 browser 和 UI

所以需裝 xwindow 或 Xvfb

#### firefox

```shell
sudo apt search firefox

sudo apt-get install firefox firefox-locale-en
```

如果顯示

```shell
Gtk-WARNING **: Locale not supported by C library.
    Using the fallback 'C' locale.
```

請設定 locale

我是設定 en_US

```shell
export LC_ALL=en_US.UTF-8
```

#### ~~xvfb~~

```shell
sudo apt-get install xvfb
```shell

然後啟動與指派到哪個 port

```shell
sudo Xvfb :10 -ac
```

指定輸出的 DISPLAY

```shell
export DISPLAY=:10
firefox
```

之後再啟動測試

但

這裡就遇到問題了

出現錯誤訊息...

```shell
Error: no display specified
```

但奇怪的是明明都 export DISPLAY 了還出這 error...

目前都還沒解決這問題...

所以直接採用下面的兩個備案

1. 裝一台有 GUI 的 Linux 到實體機器上, 非 VM

2. 使用 [SAUCE LABS](https://saucelabs.com/)

個人是建議公司肯出錢就採用 SAUCE LABS 的服務, 隨然有點小貴, 因為涵蓋的 OS 和 browser 很多, 且有 mobile web 的測試(雖然 android  都只有到 4.X 而已

下面說明一下如何設定 SAUCE LABS 與 SAUCE LABS 是如何運作的

### SAUCE LABS

SAUCE LABS 提供多個 OS 與 browser 版本的 VM 以供測試且有 native app 的測試

有 14 天的免費試用, 且有 opensource 的 free 方案

在 price 方面須注意的是 Manual 的方案是不含自動化測試的

他有提供 API 去處理測試結果與資訊, 但因為我不會用到所以就沒細看有哪些功能

基本上使用 SAUCE LABS 的流程如下

![test.png](http://user-image.logdown.io/user/3170/blog/3202/post/774036/8YR4x8nTOSagnQ0MoRx2_test.png)

基本上就是連上 SAUCE LABS 的 host 用 SAUCE LABS 的 VM 測試

下面會說一下設定方式

跟跑 webdriver 一樣設定可分兩種去 run

1. Standalone Mode

2. The WDIO Testrunner

1 可參考官方文件

[Node.js Test Setup Example - The Sauce Labs Cookbook - Sauce Labs Documentation Wiki](https://wiki.saucelabs.com/display/DOCS/Node.js+Test+Setup+Example)

我是採用 2

所以需追加的設定是

```json
capabilities: [{
    'browserName': 'chrome',
    'platform': 'Windows 10',
    'username': <username>,
    'accessKey': <accessKey>
}],

host: <username> + ':' + <accessKey> + '@ondemand.saucelabs.com',
port: 80,
path: '/wd/hub',

```

`<username>` 和 `<accessKey>` 都可以經由 SAUCE LABS 後台取得

這樣就可以使用 SAUCE LABS 來跑測試程式了

### Note

當你一段時間沒跑, 之後又再跑時有錯

有可能向我遇到JAVA 更新

那這時 `Selenium Standalone Server` 就要更新 [Link](http://www.seleniumhq.org/download/)

browser driver 也要更新

[2016 JSDC 淺談網站自動化測試](http://slides.com/alincode/jsdc2016_webdriverio/fullscreen#/)
