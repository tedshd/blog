---
title: "HTML form submit same name in php, nodejs, golang"
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

## PHP

以下問答有提供了 PHP [doc](https://www.php.net/manual/en/faq.html.php#faq.html.arrays) 說明 PHP 如何處理多選

[PHP Multiple Checkbox Array](https://stackoverflow.com/questions/14026361/php-multiple-checkbox-array)

在 name 後面添加 `[]` 即可處理把相同的 name 組成 Array

沒有加的話是會取**最後一個**

POST & GET 都是如此處理

example:

```html
<input type="checkbox" name="game[]" value="FGO" />
<input type="checkbox" name="game[]" value="GirlsFrontline" />
```

```php
<?php
$_GET['game'];
$_POST['game'];
```

## nodejs

GET 和 POST 用的方式不一樣

基本上都會用到 `querystring` module

`querystring` module 主要都在處理 querystring 相關的功能

主要靠它 parse querystring format(ex: key=calue&key2=value2)

所以 nodejs 會自動把同樣的 name 併在一起組成 array

### GET

會需要用 `url` module

`url` module 主要是要拿掉 GET 的 url 的 querystring 再丟給 `querystring` 處理

example:

```html
<input type="checkbox" name="game" value="FGO" />
<input type="checkbox" name="game" value="GirlsFrontline" />
```

```js
const url = require("url");
const querystring = require("querystring");

const thisUrl = new URL(req.url, "http://" + req.headers.host);
const query = new URLSearchParams(thisUrl.search).toString(); // 這一段是要把 `?key=calue&key2=value2` => `key=calue&key2=value2`

querystring.parse(query)["game"];
```

### POST

把接進來的 body 組起來再使用 `querystring` parse

example:

```js
var formData = "";
req.on("data", function (data) {
  formData += data;
});
req.on("end", function () {
  console.log(querystring.parse(formData)["game"]);
});
```

[URL | Node.js v15.0.1 Documentation](https://nodejs.org/api/url.html)

[Query string | Node.js v15.0.1 Documentation](https://nodejs.org/api/querystring.html)

## golang

import `http` 就可以處理 GET 和 POST 的情況

大致上的處理方式和行為和 nodejs 一樣(只差在語言的寫法不一樣)

也是會自動把同樣的 name 併在一起

組成 slice

### GET

request struct 裡面有 URL 有 function `Query` 可以拿到所有的 querystring

example:

```html
<input type="checkbox" name="game" value="FGO" />
<input type="checkbox" name="game" value="GirlsFrontline" />
```

```go
package main

import (
    "fmt"
	"net/http"
)

func getHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Println(r.URL.Query()["game"])
}

func main() {
    http.HandleFunc("/get", getHandler)
}
```

### POST

request 有一個 `parseForm` 的 function 可以抓取 HTTP `POST`, `PUT`, and `PATCH` 的 body

example:

```go
package main

import (
    "fmt"
	"net/http"
)

func postHandler(w http.ResponseWriter, r *http.Request) {
    r.ParseForm()
    fmt.Println(r.Form["game"])
}

func main() {
    http.HandleFunc("/post", postHandler)
}
```

[http - parseForm](https://golang.org/pkg/net/http/#Request.ParseForm)

## 最後總結

**只有 PHP 要在相同的 name 後面添加 `[]` 才可以在 PHP 端收到的 name 併在一起**

**nodejs 和 golang 都只要是 name 一樣就可以了**

針對這三種語言都有寫了 demo code

只要三種語言的環境裝好

都可以直接起 local server 來試驗看看

[html_form_multiple_name](https://github.com/tedshd/html_form_multiple_name)
