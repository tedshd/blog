---
layout: post
title: 'AJAX - XMLHttpRequest Introduction'
date: 2015-01-10
comments: true
categories: [javascript, Ajax]
---
## AJAX - XMLHttpRequest Introduction

### Intro

說到 AJAX 行為就不行不提到 XMLHttpRequest object

不知道現在的前端工程師還有人認識這個東西嗎?

當前 library 眾多(YIU, jQuery, AngularJS, Backbone.js...)

可能用過

* `Y.jsonp(url, callback);`
* `$.ajax();`
* `$http();`
* ......

這些處理 AJAX 行為的 method

這些 library 在處理 AJAX 行為時其實都是 base on XMLHttpRequest

所以就來簡單說明一下這玩意, 了解這東西其實有助於處理 AJAX 行為

因為這算是在前端開發上會較接觸到網路 http Protocol 的東西, 也跟後端有較緊密的關係

### History

其實在早期 XMLHttpRequest 尚未定案下來時也有許多名稱

```javascript
var httpRequest;
if (window.XMLHttpRequest) {
    // IE7,Mozila,Safari...
    httpRequest = new XMLHttpRequest();
} else if (window.ActiveXObject) {
    // IE5,IE6
    // 找出最新版MSXML剖析器
    var msxmls = ["MSXML2.XMLHttp.4.0","MSXML2.XMLHttp.3.0","MSXML2.XMLHttp","Mircosoft.XMLHttp"];
    for (i = 0; i < msxmls.length; i++) {
        try {
            // 建立XMLHttpRequest物件
            httpRequest = new ActiveXObject(msxmls[i]);
            break;
        } catch (e) {
            // do something
        }
    }
}
```

相信看過這段 code 的人大概都會會心一笑

在早期確實還是要去判斷該物件是否存在來兼容各 browser

在處理 AJAX 上也不像現在都包好好, 都是自己處理許多行為, 但這樣也會較了解真實運作的原理

```javascript
var xhr = new XMLHttpRequest();

xhr.open('GET', 'example.html', true);
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
        document.getElementById('myDiv').innerHTML = xhr.responseText;
    }
};
xhr.send();
```

上列為早期最簡單的一個 AJAX 行為

從上面的 code 就可以看出要用 GET 來作取資料的動作, 所以就必須了解 http 原來有 GET, POST, DELETE, PUT 等等的 method

從 `xhr.status` 可以了解到原來 http Protocol 有定義許多 status code 來表示 request 最後 response 的狀態

甚至許多人大概很少處理 timeout, abort, setRequestHeader

其實都有定義, 而要有一個嚴謹的 AJAX 行為其實並不是單純的使用 library 處理 success 或 error, 其實有很多情況要處理

必須要很了解 AJAX 的流程與許多可能發生的例外狀況

例如 padding 時間過久是否要重發還是取消, error 發生時依據 http status code 適當的 feedback 到畫面上等等都是在處理 AJAX 行為要注意的事

### Data Transfer

在使用 library 時大家都知道要帶參數到後端大部份只要把參數帶入用 json 格式包起來的 object 中就可以了, 但卻不知道其實 library 都幫忙實作好多東西了

其實有兩種方式可以帶參數到後端

* FormData
* application/x-www-form-urlencoded

但這東西說穿了就是像是利用 form 的方式來傳送資料

#### FormData

```javascript
// FormData
var formData = new FormData();
formData.append('str', 'string');
formData.append('num', 123);
var xhr = new XMLHttpRequest();
xhr.open('POST', 'test.php');
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
        document.getElementById('myDiv').innerHTML = xhr.responseText;
    }
};
xhr.send(formData);
```

PHP 部分

```php
$str = $_POST['str'];
$num = $_POST['num'];
```

#### application/x-www-form-urlencoded

```javascript
// application/x-www-form-urlencoded
var obj = {
        'user': 'ted',
        'password': '123456'
    },
    jsonData;
jsonData = JSON.stringify(obj);
var xhr = new XMLHttpRequest();
xhr.open('POST', 'test.php', true);
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
        document.getElementById('myDiv').innerHTML = xhr.responseText;
    }
};
xhr.send('json=' + jsonData);
```

PHP 部分

```php
$request_json = json_decode($_POST['json'], true);
```

較常用的方式會是建立 FormData 的方式來處理

但由於 IE 10 以上才支持 FormData

所以在未支援的情況下建議使用 `application/x-www-form-urlencoded` 的方式

關於一些 AJAX 的進階應用與 request/response 行為以後會有文章說明
