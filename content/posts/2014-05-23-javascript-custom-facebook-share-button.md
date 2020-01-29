---
layout: post
title: 'JavaScript - custom facebook share button'
date: 2014-05-23
comments: true
categories: [javascript, facebook]
---
## JavaScript - custom facebook share button

<strong style="color:red">
Before use facebook API, must create facebook app on facebook's [developer website](https://developers.facebook.com/) to get a app id
</strong>

Facebook support share API to people and it is easy to use.
But sometimes we need customize share button style in our web.
We can use 2 way.

## 1. Link share api link

Simple way

### HTML

```html
<a href="http://www.facebook.com/share.php" class="custom">Share</a>
```

and then you can use CSS custom `a` style.

But this only can catch current url to share to facebook.

## 2. Use facebook JavaScript SDK

This way is powerful

### HTML

```html
<div id="fb-root"></div>
<a href="http://www.google.com/" data-image="Article img url" data-title="Article Title" data-desc="Some description for this article" class="fb_share">
	<img src="http://www.synermous.com/data/images/fb-icon.svg" alt="" width="50" height="50">
</a>
```

### JavaScript

```javascript
window.fbAsyncInit = function() {
    FB.init({
        appId: <your facebook app id>,
        status: true,
        cookie: true,
        xfbml: true
    });
};

(function(d, debug){var js, id = 'facebook-jssdk', ref = d.getElementsByTagName('script')[0];if   (d.getElementById(id)) {return;}js = d.createElement('script'); js.id = id; js.async = true;js.src = "//connect.facebook.net/en_US/all" + (debug ? "/debug" : "") + ".js";ref.parentNode.insertBefore(js, ref);}(document, /*debug*/ false));

function postToFeed(title, desc, url, image) {
    var obj = {method: 'feed',link: url, picture: image,name: title,description: desc};
    function callback(response) {}
    FB.ui(obj, callback);
}

var fbShareBtn = document.querySelector('.fb_share');
fbShareBtn.addEventListener('click', function(e) {
    e.preventDefault();
    var title = fbShareBtn.getAttribute('data-title'),
        desc = fbShareBtn.getAttribute('data-desc'),
        url = fbShareBtn.getAttribute('href'),
        image = fbShareBtn.getAttribute('data-image');
    postToFeed(title, desc, url, image);

    return false;
});
```

This way can customize share url facebook og information
`href` = url you want share, must have link
`data-image` = image you want show on facebook, if not value it can catch origin og
`data-title` = title you want show on facebook, if not value it can catch origin og
`data-desc` = description you want show on facebook, if not value it can catch origin og

[facebook opengraph](https://developers.facebook.com/docs/opengraph)
[custom facebook share button](http://stackoverflow.com/questions/22037021/custom-facebook-share-button)
