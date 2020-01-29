---
layout: post
title: 'Facebook api get UID & AccessToken'
date: 2013-11-25
comments: true
categories: [facebook, javascript]
---
## Facebook api get UID & AccessToken

1. Build App in facebook
2. ```APP_ID``` is a facebook App id
3. Must set facebook App's web url and use code in it's domain

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>fb_oauth</title>
<script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>
</head>
<body>
    <div id="fb-root"></div>
    <p>
        <input id="FBLogin" type="button" value="登入臉書" />
    </p>
    <p>
        <span id="uid"></span>
    <br>
        <span id="accessToken"></span>
    </p>
</body>
<script src="http://connect.facebook.net/zh_TW/all.js"></script>
<script>
    FB.init({
        appId: 'APP_ID',
        status: true,
        cookie: true,
        xfbml: true,
        oauth: true
    });
    $('#FBLogin').click(function () {
        FB.login(function (response) {
            // 登入之後執行的語法
        },
        {
            scope: 'email'
        });
    });
    FB.getLoginStatus(function (response) {
        if (response.status === 'connected') {
            // 程式有連結到 Facebook 帳號
            // 取得 UID
            var uid = response.authResponse.userID;
            // 取得 accessToken
            var accessToken = response.authResponse.accessToken;
            $('#uid').html('UID：' + uid);
            $('#accessToken').html('accessToken：' + accessToken);
        } else if (response.status === 'not_authorized') {
            // 帳號沒有連結到 Facebook 程式
            alert('請允許授權！');
        } else {
            // 帳號沒有登入
        }
    });
</script>
</html>
```

[Demo](http://tedshd.lionfree.net/demo/facebook_oauth/fb_oauth.html)

[Refer - 使用 Facebook JavaScript SDK 來取得使用者 UID 或 AccessToken](http://coding.anyun.tw/2012/03/07/using-facebook-javascript-sdk-get-uid-or-accesstoken/)
