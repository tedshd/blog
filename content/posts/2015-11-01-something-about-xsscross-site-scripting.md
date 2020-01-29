---
layout: post
title: 'Something about XSS(Cross-site scripting)'
date: 2015-11-01
comments: true
categories: [xss, php, javascript]
---
## Something about XSS(Cross-site scripting)

If not set anything

Use like

```php
<?php echo $_GET['name'];?>
```

and querystring `name` = `<script>alert(document.cookie)</script>`

And not defence XSS

In Firefox

![螢幕快照 2015-11-01 下午8.40.08.png](http://user-image.logdown.io/user/3170/blog/3202/post/307308/G2Ec0H05TgG5yNFaRS6K_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-11-01%20%E4%B8%8B%E5%8D%888.40.08.png)

In Chrome

![螢幕快照 2015-11-01 下午8.42.45.png](http://user-image.logdown.io/user/3170/blog/3202/post/307308/tyAndfVzTqy50xBAJmhI_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-11-01%20%E4%B8%8B%E5%8D%888.42.45.png)

In Safari

![螢幕快照 2015-11-01 下午8.43.16.png](http://user-image.logdown.io/user/3170/blog/3202/post/307308/xfWYDtAnQ7SoVIKdlTIL_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-11-01%20%E4%B8%8B%E5%8D%888.43.16.png)

### Result

Chrome & Safari browser has handle XSS default

### Defence

Set header `X-XSS-Protection: 1`

if use PHP, can use

```php
htmlspecialchars()
// or
 htmlentities()
```

### Important!

Finally

We must know it is handle encode to avoid run JavaScript on page

[JavaScript ver htmlspecialchars](https://github.com/tedshd/javascript-htmlspecialchars)

[Refer - XSS攻擊的深入探討與防護之道](http://www.qa-knowhow.com/?p=2992)
