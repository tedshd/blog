---
title: "Form_multi_checkbox_checked_in_php_nodejs_golang"
date: 2020-10-24T15:39:19+08:00
draft: false
categories: [HTML, form, php, go, golang, nodejs]
---

一直以來大部分時間都在用 PHP 開發

所以也用 PHP 來處理 HTML Form

所以都下意識地認為 `<input type="checkbox" name="game[]" value="FGO">`

這樣的 `name="game[]"` 的處理方式是正規的處理 HTML Form 的多選的方式

也疑惑為何大多的 HTML Form 的教學甚至 MDN 都沒有提到這件事

就在某一天我在檢視到同事寫的 code 時

發現同事用 JavaScript 處理

硬爬出來自己組字串送出去

我才想起這令人感到恐懼的事情

因為公司同事是寫 golang 的專門, 就算前端不熟

應該也不至於連這樣概念都沒有就用硬爬的方式處理

所以再調整的同時也跟同事確認後

我也真正的直視這問題

到底要怎麼處理表單中多選的資料?

PHP 寫久的人大多都知道要用上面列出的方法

`name="game[]"`

就是 `game` + `[]`

但是當我認真地尋找關於這個問題時

意外地發現了一篇 stackoverflow 的問答

[Several Checkboxes sharing the same name](https://stackoverflow.com/questions/16552680/several-checkboxes-sharing-the-same-name)

其實 W3C 根本沒有管你 name="" 重複要如何處理

以下是 PHP, nodejs, golang 的原生方式來測試的結果

## 關於 PHP 的部分

以下問答有提供了 PHP [doc](https://www.php.net/manual/en/faq.html.php#faq.html.arrays) 說明 PHP 如何處理多選

[PHP Multiple Checkbox Array](https://stackoverflow.com/questions/14026361/php-multiple-checkbox-array)

### 結果

在 name 後面添加 `[]` 即可處理把相同的 name 組成 Array

POST & GET 都是如此處理

## nodejs

nodejs

可以用

## golang

golang 的 `http` 有一個 `parseForm` 的 function 可以抓取 HTTP `POST`, `PUT`, and `PATCH` 的 body

它會自動把相同的 name 整合起來變成 array

但是這在 `GET` 的情況就無法處理了, 因為 GET 沒有 body

[http - parseForm](https://golang.org/pkg/net/http/#Request.ParseForm)
