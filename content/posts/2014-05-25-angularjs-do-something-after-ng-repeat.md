---
layout: post
title: 'AngularJS - do something after ng-repeat'
date: 2014-05-25
comments: true
categories: [AngularJS, javascript]
---
## AngularJS - do something after ng-repeat

在學習用 AngularJS 的過程中遇到個問題就是
ng-repeat 好厲害喔, code 變得好少喔
但我想再 ng-repeat 完移掉 loading view 要怎麼移啊?
用 `setTimeout` 跟白癡一樣, 又不知道時間要設多久
只好向 fb 求救
沒想到有人立馬給出解決方案
[原文來源 blog](http://www.nodewiz.biz/angular-js-final-callback-after-ng-repeat/)

由於對 AngularJS 不是了解的很透徹, 所以在此不詳加說明(原文內有說明)
這裡只上 code

### HTML

```html

<div id='list' ng-app="testApp">
    <div ng-controller="blogger" >
        <ul>
            <li ng-repeat="list in blog"  on-last-repeat>
                {{list.title.$t}}
            </li>
        </ul>
    </div>
</div>

```

### JavaScript

```javascript

var module = angular.module('testApp', [])
     .directive('onLastRepeat', function() {
        return function(scope, element, attrs) {
            if (scope.$last) setTimeout(function(){
                scope.$emit('onRepeatLast', element, attrs);
            }, 1);

        };
    })

.controller('blogger', function($scope, $http, $parse) {
        $scope.$on('onRepeatLast', function(scope, element, attrs){
        alert(document.querySelector('#list').offsetHeight + 'px');
      });

         // json callback must JSON_CALLBACK
        $http.jsonp('http://tysh310246.blogspot.com/feeds/posts/default?alt=json&callback=JSON_CALLBACK').success(
            function(data) {
                $scope.blog = data.feed.entry;
            }
        );


});

```

這段 code 最後 `alert` 的高度是 `ng-repeat` 完後 list 的高度
