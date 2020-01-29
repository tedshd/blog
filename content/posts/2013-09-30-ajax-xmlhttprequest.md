---
layout: post
title: 'AJAX - XMLHttpRequest'
date: 2013-09-30
comments: true
categories: [javascript]
---
## AJAX - XMLHttpRequest

Use XMLHttpRequest object handle AJAX

client -> server
Front-end - request -> back-end
client <- server
Front-end <- response - back-end

### ~~build XMLHttpRequest~~(old method)
**JavaScript**
```javascript
var httpRequest;
if (window.XMLHttpRequest) {
    //IE7,Mozila,Safari...
    httpRequest = new XMLHttpRequest();
} else if (window.ActiveXObject) {
    //IE5,IE6
    //找出最新版MSXML剖析器
    var msxmls = ["MSXML2.XMLHttp.4.0","MSXML2.XMLHttp.3.0","MSXML2.XMLHttp","Mircosoft.XMLHttp"];
    for (i = 0; i < msxmls.length; i++) {
        try {
            //建立XMLHttpRequest物件
            httpRequest = new ActiveXObject(msxmls[i]);
            break;
        } catch (e) {
            // do something
        }
    }
}
```

<span style="color:red;font-weight:bold;">New browser have XMLHttpRequest object now.</span>
[MDN](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
**JavaScript**
```javascript
var xmlHttpRequest = new XMLHttpRequest();
```

### 2 type to post data to backend(send request)

1 **FormData**(if IE, 10 up)
```javascript
// init FormData
var formData = new FormData();
// add data
formData.append('user', 'Ted_Shiu');
formData.append('password', '123456');
// init XMLHttpRequest
var xmlHttpRequest = new XMLHttpRequest();
// build poet method and backend target
xmlHttpRequest.open('POST', 'ajax.php');
// send request
xmlHttpRequest.send(formData);
```
2 **JSON**
```javascript
// obj is data want to post to backend
var obj = {
        'user': 'ted_shiu',
        'password': '123456'
    },
    jsonData;
// init XMLHttpRequest
var xmlHttpRequest = new XMLHttpRequest();
// build poet method and backend target
xmlHttpRequest.open('POST', 'json.php');
// build content type
xmlHttpRequest.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
// obj to url string
function formUrlEncode(obj) {
    var urlData = '';
    for (var x in obj) {
        urlData = urlData + x + '=' + obj[x] + '&';
    }
    urlData = urlData.substr(0, (urlData.length - 1));
    return urlData;
}
// send request
xmlHttpRequest.send(formUrlEncode(obj));
// if want ajax get data
// use xmlHttpRequest.send();
// xmlHttpRequest.send('user=ted_shiu&password=123456');
```

### Backend(handle request and response browser)
**PHP**
```php
// ajax.php
<?php
    if (isset($_POST['user'])) {
        // do something
        if ($_POST['password']) {
            // do something
            $output = array(
                'status' => 'ok',
                'message' => 'msg'
            );
            // echo is reponse browser, must use json_encode()
            echo json_encode($output);
        }
    }
?>
// json.php
<?php
var_dump($_POST);
echo '<br>';
echo $_POST['user'];
echo '<br>';
echo $_POST['password'];
?>
```

[Refer - 你不可不知的 JSON 基本介紹](http://blog.wu-boy.com/2011/04/%E4%BD%A0%E4%B8%8D%E5%8F%AF%E4%B8%8D%E7%9F%A5%E7%9A%84-json-%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%B4%B9/)
[Refer - Ajax and JSON](http://coursesweb.net/ajax/ajax-json)

### Response
AJAX handle response from backend
check response state, use XMLHttpRequest properties
```javascript
xmlHttpRequest.onreadystatechange = function() {
    if (xmlHttpRequest.readyState == 4) {
        // do something
        if (xmlHttpRequest.status == 200) {
            alert(xmlHttpRequest.responseText);
            // parse response to object
            var data = JSON.parse(xmlHttpRequest.responseText);
            alert(data.status);
        }
    }
}
```
