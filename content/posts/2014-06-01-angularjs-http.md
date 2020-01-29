---
layout: post
title: 'AngularJS - $http'
date: 2014-06-01
comments: true
categories: [javascript, AngularJS]
---
## AngularJS - $http

Angular use $http handle AJAX behavior.
It support method to handle rest API and basic usage.
**But its default `Content-type` is `application/json`**

### Basic usage

```javascript
$http({
    method: 'GET', // support GET, POST, PUT, DELETE
    url: '../php/response.php',
    params: data, // GET method query string
    data: data,
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'
    },
    timeout: 30000, // timeout abort AJAX
    cache: false
}).
success(function(data, status, headers, config) {
    // this callback will be called asynchronously
    // when the response is available
    console.log(data);
}).
error(function(data, status, headers, config) {
    // called asynchronously if an error occurs
    // or server returns response with an error status.
    console.error(data);
});
```

[Refer - $http](https://docs.angularjs.org/api/ng/service/$http#usage)
[Refer - AngularJS AJAX](http://tutorials.jenkov.com/angularjs/ajax.html)

### get, post, put, delete, head, jsonp

data is a object like

```javascript
var data = {user: 'Ted', pwd: 12345};
```

#### $http.get(url, config)

#### $http.post(url, data,config)

#### $http.put(url, data, config)

#### $http.delete(url, config)

#### $http.head(url, config)

#### $http.jsonp(url, config)

jsonp url must add callback

```javascript
$http.jsonp(url + '?callback=JSON_CALLBACK').
success(function(data, status, headers, config) {
    console.log(data);
    // this callback will be called asynchronously
    // when the response is available
}).
error(function(data, status, headers, config) {
    // called asynchronously if an error occurs
    // or server returns response with an error status.
    console.error(data);
});
```

### PHP handle request

#### rest API

Beacuse AngularJS default request `Content-type` is `application/json`
So we must use `json_decode`

```php
<?php

$request = file_get_contents("php://input");
$method = $_SERVER['REQUEST_METHOD'];
switch($method)
{
    case "PUT":
        print_r($method);
        echo '<br>';
        print_r(json_decode($request, true));
        echo '<br>';
        print_r(json_decode($request, true)['user']);
    break;
    case "GET":
        print_r($method);
        print_r($_GET);
        echo '<br>';
        print_r($_GET['user']);
    break;
    case "DELETE":
        print_r($method);
        echo '<br>';
        print_r(json_decode($request, true));
        echo '<br>';
        print_r(json_decode($request, true)['user']);
    break;
    case "POST":
        print_r($method);
        echo '<br>';
        print_r(json_decode($request, true));
        echo '<br>';
        print_r(json_decode($request, true)['user']);
    break;
}

?>
```

#### Other way(only use GET & POST)

Set `Content-type` as `application/x-www-form-urlencoded; charset=UTF-8`

1. Set all request as 'application/x-www-form-urlencoded; charset=UTF-8'

```javascript
var module = angular.module('module', []);
module.config(function($httpProvider) {
	$httpProvider.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded; charset=UTF-8';
});
```

2. Set request header if it need

```javascript
$http({
    method: 'POST',
    url: '../php/response.php',
    data: data,
    headers: {'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'}
}).
success(function(data, status, headers, config) {
    // this callback will be called asynchronously
    // when the response is available
    console.log(data);
}).
error(function(data, status, headers, config) {
    // called asynchronously if an error occurs
    // or server returns response with an error status.
    console.error(data);
});
```

And then data is stringify object like

```javascript
var data = {user: 'Ted', pwd: 12345};
data = 'data=' + JSON.stringify(data);
```

So php is

```php
<?php

$data = json_decode($_POST['data'], true);
echo $data['user'];
// or
$data = json_decode($_GET['data'], true);
echo $data['user'];

?>
```

[Refer - Angular HTTP post to PHP and undefined](http://stackoverflow.com/questions/15485354/angular-http-post-to-php-and-undefined/)

[HTTP 標頭參照](http://msdn.microsoft.com/zh-tw/library/aa287673(v=vs.71).aspx)
