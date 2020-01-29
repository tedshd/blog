---
layout: post
title: 'Firebase - Firebase functions 使用紀錄'
date: 2019-12-20
comments: true
categories: [firebase, functions]
---
## Firebase - Firebase functions 使用紀錄

最近想把一些自己在用的小東西丟到 severless 的服務

因為之前發生過一次 server 掛掉過一次的情況

當時是 GCP CE 不知為何 VM 中的網卡設定出問題

整個網卡消失

然後外部根本連不進去

最後請教大大後

只好開一個新的 instance 然後把原本的那個儲存空間掛到新開的 instance

因為那台平常在試驗的 server

裡面亂七八糟而且大多的 code 都不會做 git 控管

所以就想說把一些常用的功能用 serverless 拆出來好了

就想說來研究一下火了一陣子然後設定沒設定好就會噴一堆預算和安全性問題的 Firebase 所推出的 [functions](https://firebase.google.com/docs/functions)

其實 GCP 自己本身也有 cloud functions

但我這是玩票性質的

所以就先用 firebase functions 來試試啦

先說一下目前 firebase functions 只支援 Nodejs

但是 Google cloud 的 [cloud functions](https://cloud.google.com/functions/docs/writing/) 支援 Nodejs python golnag

1. 首先先裝 firebase-tools CLI

```shell
npm install -g firebase-tools
```

2. 執行 firebase login

```shell
firebase login
```

3. 到要建立 functions 的資料夾

這時候要注意如果你要做版本控管

就是直接到該 repository 的目錄下即可

下一步會在這目錄建立需要的程式

4. 執行 firebase init functions

```shell
firebase init functions
```

過程中會請你選擇或新開專案

這邊的專案是指 firebase 上面的專案

可以用 `JavaScript` 寫或 `TypeScript` 寫 code

整個 functions 的結構

```
myproject
 +- .firebaserc    # Hidden file that helps you quickly switch between
 |                 # projects with `firebase use`
 |
 +- firebase.json  # Describes properties for your project
 |
 +- functions/     # Directory containing all your functions code
      |
      +- .eslintrc.json  # Optional file containing rules for JavaScript linting.
      |
      +- package.json  # npm package file describing your Cloud Functions code
      |
      +- index.js      # main source file for your Cloud Functions code
      |
      +- node_modules/ # directory where your dependencies (declared in
                       # package.json) are installed
```

### 要注意的事和開始寫扣啦

index.js 就是 functions 會執行的程式

你可以依照自己的需求安裝需要的 node 套件

但需要注意的是該套件安裝完你的 `package.json` 的 `dependencies` 必須有紀錄該套件的版號

`package.json` 中的

```json
"engines": {
  "node": "8"
}
```

表示使用的 node 版本

目前預設是 8

10 有支援但目前是 beta

可以看目前[文件](https://firebase.google.com/docs/functions/manage-functions#set_nodejs_version)來決定用哪一版的 nodejs

```JavaScript
exports.ok = functions.https.onRequest((request, response) => {
 response.send("Hello from Firebase!");
});
```

ok 就會是實際上 url path

上線後的 url 會是

```
http://<region>-<firebase project name>.cloudfunctions.net/<exports name>

ex:
http://us-central1-my-project.cloudfunctions.net/ok
```

相關 [API](https://firebase.google.com/docs/reference/functions) 可以參考

很多 API 都和 express 幾乎一樣

如果要帶參數的話可以用 [params](https://expressjs.com/en/api.html#req.params)

### 部署區域

可以決定該功能在那個區域部署

同一個 index 檔案可以部署不同地區

預設是 us-central1 (Iowa) 艾荷華

可以查看[支援的 region 列表](https://firebase.google.com/docs/functions/locations)

只要添加在 code 之中即可

```Javasctipt
exports.ok = functions.region('asia-northeast1').https.onRequest((request, response) => {
...
```

目前沒法在程式中直接設定 multi region 得一個一個上

不然官方是建議建立不同 region 的 entry

[modify-region](https://firebase.google.com/docs/functions/manage-functions#modify-region)

再把 function 邏輯抽象出來就可以了

### 本地測試

可以參考[Run functions locally](https://firebase.google.com/docs/functions/local-emulator)

會在本地開啟 local server

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F螢幕快照_2019-12-20_下午2_12_47.png?alt=media&token=f2b94428-cd21-4452-8718-c6aceb378c08)

也會有對應的 url path 可以讓你直接點

如果要測試 log

在 node 中寫

```JavaScript
console.log()
console.info()
console.error()
console.warn()
```

就可以了

### 呼叫第三方或外部 api 時出現 EAI_AGAIN

查了一下

這是 DNS 解析的問題

在 Free 方案只允許呼叫 Google service 自己的 api

要切到付費方案才可以

用 Blaze plan 就可以了

[Refer - getaddrinfo EAI_AGAIN api.sendgrid.com:443](https://github.com/sendgrid/sendgrid-nodejs/issues/927)
