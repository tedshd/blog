---
layout: post
title: 'PHP - Auto update static files cache'
date: 2015-08-16
comments: true
categories: [php, css]
---
## PHP - Auto update static files cache

We can cache static files(CSS, JavaScript) to client

When Server update static code.

We want to update cache then we can modify file or add query string update version.

We have some choice like modify url `?v=1` to `?v=2`

But I want to auto modify version.

This is a way i use

```php

<?php
function autoversion($url) {
    $ver = stat($_SERVER['DOCUMENT_ROOT'] . $url)[mtime];
    return $url . "?v=" . $ver;
}
# example
?>

<link href="<?php echo autoversion('/path/to/theme.css'); ?>" rel="stylesheet">
```

This way use file last modify time as a version.

~~First i want to use `filemtime` but it fail.~~

~~So i give up this way.~~

### Update

Before use `filemtime()`, must use `clearstatcache();`

And my friend say `stat` has IO behavior, so this way is not perfect solution.

If service has lot of `stat()` or mass request, so many IO can influences performance.

Then we can write a script add update version and run it when service deploy.

[Refer - Strategies for Cache-Busting CSS](https://css-tricks.com/strategies-for-cache-busting-css/)

[Refer - stat](http://php.net/manual/en/function.stat.php)

[filemtime](http://php.net/manual/en/function.filemtime.php)
