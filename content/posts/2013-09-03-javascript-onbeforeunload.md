---
layout: post
title: 'JavaScript - onbeforeunload'
date: 2013-09-03
comments: true
categories: [javascript]
---
## onbeforeunload

onbeforeunload 是在 browser 在轉換頁面時會觸發的事件
當有 return 值時, 會出現 confirm 視窗, 並停住觸發的行為
目前試過會觸發的行為有

* 上一頁 / 下一頁
* 重新整理
* 關閉視窗
* 前往其它 URL
* submit 事件
* URL 改變時

這幾種較常見
用法如下

```javascript
var fun = function () {
    return 'Exit?';
}
window.onbeforeunload = fun;
```

return 的值是 confirm 的訊息
可 return **string** or **array**
無法 return **fuinction**

也可以用條件判斷

```javascript
var fun = function () {
    var value = document.getElementsByTagName('textarea')[0].value;
    if (value) {
        return 'Exit?';
    }
    return;
}
window.onbeforeunload = fun;
```
上面說明了當 textarea 有值時, 觸發 onbeforeunload 才 return 訊息出來

### Issue

當使用 ```<a href=""></a>``` 時, 通常會用 ```<a href="#"></a>``` or ```<a href="javascript:void(0)"></a>``` 來使 href 沒有作用, 但用 # 會在 URL 的最後產生 # , 且頁面會捲動到頂部, 這是因為 ＃ 的特性, 所以通常不會用 ```<a href="#"></a>```

但是當使用 ```<a href="javascript:void(0)"></a>``` 時, 再與 onbeforeunload 一起用時就會有問題

[demo](http://tedshd.lionfree.net/demo/onbeforeunload/onbeforeunload_void(0)_2.html)
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>onbeforeunload_javascript.void(0)</title>
<script>
var fun = function () {
    return 'exit?';
}
window.onbeforeunload = fun;
</script>
</head>
<body>
    <a href="javascript:void(0)">javascript:void(0)</a>
</body>
</html>
```

上面的 HTML 在執行時都沒問題, 但是在 **IE** 中, 會把 href="javascript:void(0)" 當成一個無效的連結
所以就觸發了 onbeforeunload 事件
而解決辦法也很簡單, 就是 **e.preventDefault()**

* JavaScript(IE9 up)
[demo](http://tedshd.lionfree.net/demo/onbeforeunload/onbeforeunload_void(0).html)
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>onbeforeunload_e.preventDefault()</title>
</head>
<body>
    by javascript<br>
    <a href="javascript:void(0)">e.preventDefault()</a>
</body>
<script>
    var fun = function () {
        return 'exit?';
    }
    window.onbeforeunload = fun;
    var tag = document.getElementsByTagName('a')[0];
    tag.addEventListener('click', function (e) {
        e.preventDefault();
    });
</script>
</html>
```

* jQuery
[demo](http://tedshd.lionfree.net/demo/onbeforeunload/onbeforeunload_preventDefault().html)
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>onbeforeunload_e.preventDefault()</title>
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script>
$(function () {
    var fun = function (e) {
        return 'exit?';
    }
    window.onbeforeunload = fun;
    $('a').on('click', function (e) {
        e.preventDefault();
    });
});
</script>
</head>
<body>
    <a href="javascript:void(0)">e.preventDefault()</a>
</body>
</html>
```

[Refer](http://xieyu.blog.51cto.com/213338/55796)
[MDN](https://developer.mozilla.org/en-US/docs/Web/API/window.onbeforeunload)
