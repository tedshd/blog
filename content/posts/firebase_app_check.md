---
title: "Firebase app check 使用紀錄"
date: 2022-10-31T10:31:56+08:00
draft: false
categories: [firebase]
---

## 前言

因為公司有使用部分的 firebase 服務

那就順便用一下前一陣子推出的 [app check](https://firebase.google.com/products/app-check) 的服務(雖然我覺得這服務還沒到完善的地步)

這服務主要是要協助驗證來自 client 的請求是否合法

不只單純是 firebase 的服務可以用

一般 API 也可以使用

## 使用

目前 SDK 只支持 Node.js

[Verify App Check tokens from a custom backend](https://firebase.google.com/docs/app-check/custom-resource-backend)

因為原本的後端不是 Node 的環境

所以使用 Node.js 建立起一個 middleware 以便讓原有的 API server 來串接

## 流程

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/blog%2Ffirebase%20app%20check-Copy%20of%20Page-1.drawio.png?alt=media&token=c8d0b7ee-875f-4380-b4e9-66c33796a990)

## 所需作業

app 需要使用相關對應的 SDK

在 firebase console 把 app check 選單中建立的 app 做註冊

因為是改為單獨建立 Node.js 的服務

所以會針對文件範例做調整

```JavaScript
const http = require('http');
const url = require('url');

var admin = require('firebase-admin');

var serviceAccount = require(__dirname + '/serviceAccountKey.json');

admin.initializeApp({
  credential: admin.credential.cert(serviceAccount)
});


const statusOk = {
  'status': 'success'
};
const statusForbidden = {
  'status': 'Forbidden'
};
const statusUnauthorized = {
  'status': 'Unauthorized'
};

var server = http.createServer(async (request, response) => {
  const queryObject = url.parse(request.url, true).query;
  switch (request.method) {
    case 'GET':
      const appCheckToken = queryObject['token'];

      if (!appCheckToken) {
        response.writeHead(403, { 'Content-Type': 'application/json' });
        response.end(JSON.stringify(statusForbidden));
        break
      }

      try {
        const appCheckClaims = await admin.appCheck().verifyToken(appCheckToken);
        // If verifyToken() succeeds, continue with the next middleware
        // function in the stack.
        console.log('appCheckClaims', appCheckClaims);
        response.writeHead(200, { 'Content-Type': 'application/json' });
        response.end(JSON.stringify({
          ...appCheckClaims,
          ...statusOk
        }));
        break
      } catch (err) {
        console.log('err', err)
        response.writeHead(401, { 'Content-Type': 'application/json' });
        response.end(JSON.stringify(statusUnauthorized));
        break
      }
    default:
      response.writeHead(200, { 'Content-Type': 'application/json' });
      response.end(JSON.stringify(statusForbidden));
  }
});

server.listen(3300, function () {
  console.log('3300 port');
});

```

其中 `serviceAccountKey.json` 是 firebase console 中產生的

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/blog%2FScreen_Shot_2022-11-02_at_9_51_27_AM.png?alt=media&token=23519780-f442-4bfd-b1f4-db69739cbb81)

## 使用方式

可以使用 pm2 之類的服務啟動

這樣就可以用 `http://localhost?token=<app check token>` 的方式呼叫驗證

建議在內部使用, 走內部 IP 或內部網域以減少傳輸時間

直接以 rest api 的方式呼叫

## 後續升級

如果之後公司其他團隊也有其他的 firebase 的 app check 需求也可以添加參數或路由來使用各自的 firebase 專案設定來共用這個 API