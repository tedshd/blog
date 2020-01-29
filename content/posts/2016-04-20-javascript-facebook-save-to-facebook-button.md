---
layout: post
title: 'JavaScript - facebook save to facebook button'
date: 2016-04-20
comments: true
categories: [javascript, facebook]
---
## JavaScript - facebook save to facebook button

2016 F8

Facebook release new function - save to facebook

Then we can use it now

### Step 1

Go to facebook developer
[Save Button - Social Plugins - Documentation - Facebook for Developers](https://developers.facebook.com/docs/plugins/save)

### Step 2

Build or use facebook application

If you had facebook application can skip this step

If you build facebook application and you can get this code

```javascript
window.fbAsyncInit = function() {
  FB.init({
    appId      : '<YOUR APP ID>',
    xfbml      : true,
    version    : 'v2.6'
  });
};

(function(d, s, id){
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) {return;}
  js = d.createElement(s); js.id = id;
  js.src = "//connect.facebook.net/en_US/sdk.js";
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));
```

Put it in your website

### Step 3(Finally

Add `<div class="fb-save" data-uri="http://www.your-domain.com/your-page.html"></div>`

`data-uri` is your current page url

You can use this js code dynamic add url

```javascript
document.querySelectorAll('.fb-save')[0].setAttribute('data-uri', document.location.href);
```

### Demo

![螢幕快照 2016-04-20 上午11.15.59.png](http://user-image.logdown.io/user/3170/blog/3202/post/712381/4iebHGpaQISinQCS9jOg_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202016-04-20%20%E4%B8%8A%E5%8D%8811.15.59.png)

![螢幕快照 2016-04-20 上午11.16.09.png](http://user-image.logdown.io/user/3170/blog/3202/post/712381/6Q0VZKZDSFqokWePRTeZ_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202016-04-20%20%E4%B8%8A%E5%8D%8811.16.09.png)

Then it can show on facebook saved

![螢幕快照 2016-04-20 上午11.16.17.png](http://user-image.logdown.io/user/3170/blog/3202/post/712381/mreqYMbgTFqW9IaWLCTE_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202016-04-20%20%E4%B8%8A%E5%8D%8811.16.17.png)





