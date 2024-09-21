---
title: "在 cloud functions 或是 firebase functions 處理 nodejs 使用 import 的方式"
date: 2024-05-13T01:17:42+08:00
draft: false
categories: [nodejs, firebase]
---

## Intro

現在在使用 nodejs 時可以使用副檔名 **.mjs** 的方式和 `package.js` 添加 `"type": "module"` 來使用 `import` 來取代 `require`

關於這件事也是因為有許多歷史因素無法完全取代掉 `require`

但是如果我們想要在 cloud functions 或是 firebase functions 使用時就沒那麼順利

因為光是要使用 `.mjs` 就是個問題

但是參考下面的文章後發現有取巧的方式

[refer - ES6+ in Cloud Functions for Firebase #2](https://codeburst.io/es6-in-cloud-functions-for-firebase-2-415d15205468)

## Solution

先說結論

其實就是先用 babel build 完 code

最後把 build 完的 code 部署到 functions 上面

以 firebase functions 專案的例子

我自己的做法是 多建立一個 src 的目錄來當成再開發的 code

在部署前 build 到 functions 的目錄

`package.json`

添加

```json
"scripts": {
  "build": "babel src --out-dir functions"
}
```

`npm run build`

就會把 `src` 目錄的檔案編譯到 `functions` 目錄