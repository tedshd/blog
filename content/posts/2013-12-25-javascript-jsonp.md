---
layout: post
title: 'JavaScript - jsonp'
date: 2013-12-25
comments: true
categories: [javascript]
---
## JavaScript - jsonp

### If only get data(read)

Use callback

```javascript
// javascript
// build from javascript
var scriptEl = document.createElement("script");
scriptEl.src = "http://tysh310246.blogspot.com/feeds/posts/default?alt=json&callback=myFunction";
document.getElementsByTagName("head")[0].appendChild(scriptEl);
```

or

```html
<!-- html -->
<!-- embed from HTML -->
<script src="http://tysh310246.blogspot.com/feeds/posts/default?alt=json&callback=myFunction"></script>
```

myFunction is callback function handle json data

```javascript
// javascript
function myFunction(data) {
    // data is json
    console.log(data);
}
```

#### example

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Examples</title>
<!-- <script src="http://tedshd.lionfree.net/demo/php/api_test.php?callback=test"></script> -->
<script>
    var scriptEl = document.createElement("script");
    scriptEl.src = "http://tedshd.lionfree.net/demo/php/api_test.php?callback=test";
    document.getElementsByTagName("head")[0].appendChild(scriptEl);
    var test = function(data) {
        console.log(data);
    }
</script>
</head>
<body>

</body>
</html>
```

PHP must support to handle jsonp

```php
// PHP
$request_json = json_encode($data, true);
echo $_GET['callback'] . "(" . $request_json . ");";
```
這樣就會回傳用 callback 包起來的 json data
由於 callback 是 url query string ,所以不是用 callback 用其他名稱也是 ok 的

### If want to write data(Save)

Use XMLHttpRequest send data
[AJAX - XMLHttpRequest](http://tedshd.logdown.com/posts/143110-ajax-xmlhttprequest)

PHP 加入

```php
// PHP
header("Access-Control-Allow-Origin: *");
// header("Access-Control-Allow-Origin: http://example.com");
```

其中 * 也可改成所允許的 url

[Refer - HTTP access control (CORS)](https://developer.mozilla.org/zh-TW/docs/HTTP/Access_control_CORS)
[Refer - Server-Side Access Control](https://developer.mozilla.org/en-US/docs/Server-Side_Access_Control)
[Refer - XMLHttpRequest執行AJAX 跨網域存取](http://blog.caesarchi.com/2011/08/xmlhttprequestajax.html)
