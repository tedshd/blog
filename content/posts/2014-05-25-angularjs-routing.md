---
layout: post
title: 'AngularJS - routing'
date: 2014-05-25
comments: true
categories: [AngularJS, javascript]
---
## AngularJS - routing

這裡不探究 AngularJS 是如何辦到的
基本上就是用 hash `#`, 也可用 HTML5 的 [history API](https://developer.mozilla.org/zh-TW/docs/Web/API/Window.history)
這裡只有說有哪些用法

### 基本 sample

這寫法是 1.2.16 的寫法, 不保證以後會變(因為在舊版的 AngularJS 寫法不一樣, 差點搞死我, <strong style="color:red">當升版本後以前的 code run 不出來時最好去官方看文件</strong>)

* load AngularJS & angular-route

[AngularJS](https://angularjs.org/)
[v1.2.16](http://tedshd.lionfree.net/lib/angular_v1.2.16.js)
[angular-route](https://github.com/angular/bower-angular-route)
[backup](http://tedshd.lionfree.net/lib/angular-route.js)

* HTML

index.html

```html
<!DOCTYPE html>
<html ng-app="route">
<head>
<meta charset="utf-8">
<title>routing</title>
<script src="http://tedshd.lionfree.net/lib/angular_v1.2.16.js"></script>
<script src="http://tedshd.lionfree.net/lib/angular-route.js"></script>
</head>
<body>
    <h1>A-Mail</h1>
    <div ng-view></div>
</body>
<script src="controllers.js"></script>
</html>
```

list.html

```html
<table ng-controller="ListController">
    <tr>
        <td><strong>Sender</strong></td>
        <td><strong>Subject</strong></td>
        <td><strong>Date</string></td>
    </tr>
    <tr ng-repeat="message in messages">
        <td>{{message.sender}}</td>
        <td><a href='#/view/{{message.id}}'>{{message.subject}}</a></td>
        <td>{{message.date}}</td>
    </tr>
</table>
```

detail.html

```html
<div><strong>Subject:</strong> {{message.subject}}</div>
    <div><strong>Sender:</strong> {{message.sender}}</div>
    <div><strong>Date:</strong> {{message.date}}</div>
    <div>
        <strong>To:</strong>
        <span ng-repeat="recipient in message.recipients">{{recipient}}</span>
    </div>
    <div>{{message.message}}</div>
<a href="#/">Back to message list</a>
```

* JavaScript

controller.js

```javascript
//Create a module for our core AMail services
var aMailServices = angular.module('route', ['ngRoute']);

//Set up our mappings between URLs, tempaltes. and  controllers
function emailRouteConfig($routeProvider, $locationProvider){
    $routeProvider.
    when('/', {
        controller: ListController,
        templateUrl: 'list.html'
    }).
    // Notice that for the detail view, we specify a parameterized URL component by placing a colon in front of the id
    when('/view/:id', {
        controller: DetailController,
        templateUrl: 'detail.html'
    }).
    otherwise({
        redirectTo: '/'
    });

    // $locationProvider.html5Mode(true);
};

//Set up our route so the AMailservice can find it
aMailServices.config(emailRouteConfig);

//Some take emails
messages = [{
    id: 0, sender: 'jean@somecompany.com',
    subject: 'Hi there, old friend',
    date: 'Dec 7, 2013 12:32:00',
    recipients: ['greg@somecompany.com'],
    message: 'Hey, we should get together for lunch somet ime and catch up. There are many things we should collaborate on this year.'
},{
    id: 1, sender: 'maria@somecompany.com',
    subject : 'Where did you leave my laptop?' ,
    date: 'Dec 7, 2013 8:15:12',
    recipients: ['greg@somecompany.com'],
    message: 'I thought you were going to put it in my desk drawer. But i t does not seem to be there. '
},{
    id: 2, sender: 'bill@somecompany.com',
    subject: 'Lost python',
    date: 'Dec 6, 2013 20:35:02',
    recipients: ['greg@somecompany.com'],
    message: "Nobody panic, but my pet python is missing from her cage. She doesn't move too fast, so just call me if you see her."
}];

// Publish our messages for the list template

function ListController($scope){
    $scope.messages = messages;
}

//Get the message id fron the route (parsed from the URL) and use it to find the right message object.
function DetailController($scope, $routeParams){
    $scope.message = messages[$routeParams.id];
}
```

這裡說明一下 AngularJS 做 `$routeProvider` 時路徑會加上 hash
即 url 會是 `http://localhost/demo/angular/routing/#/` or `http://localhost/demo/angular/routing/#/view/1`

如果要移掉 hash 可參考
[Pretty URLs in AngularJS: Removing the #](http://scotch.io/quick-tips/js/angular/pretty-urls-in-angularjs-removing-the-hashtag)

需注意的是, 移 hash 後 url 需為絕對路徑, 且該頁必須有辦法為實體 url, 否則刷新後會出現該頁面不存在的訊息
