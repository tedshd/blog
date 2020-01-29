---
layout: post
title: 'Detect mobile device'
date: 2013-12-07
comments: true
categories: [php, javascript]
---
## Detect mobile device

Use PHP or JavaScript detect mobile device like iPhone, iPad, iPod or Android...

### Android

#### PHP

```php
<?php
$ua = strtolower($_SERVER['HTTP_USER_AGENT']);
if(stripos($ua, 'android') !== false) {
    echo 'Android!!';
    exit;
}
?>
```

#### JavaScript

```javascript
var ua = navigator.userAgent.toLowerCase();
if(ua.indexOf("android") > -1) {
    document.write('Android!!');
}
```

[Refer - Android Detection with JavaScript or PHP](http://davidwalsh.name/detect-android)

### Apple mobile device


[Refer - How to detect iPhone, iPod and iPad with PHP](http://php.quicoto.com/how-to-detect-iphone-ipod-and-ipad-with-php/)
[Refer - How to Identify an Apple iPhone, iPod or iPad Visitor to Your Website](http://www.sitepoint.com/identify-apple-iphone-ipod-ipad-visitors/)
