---
layout: post
title: 'gulp - One problem i found when i use CSS minify with some CSS library'
date: 2016-08-31
comments: true
categories: [gulp JavaScript CSS]
---
## gulp - One problem i found when i use CSS minify with some CSS library

When i use [pure](http://purecss.io/).

And i use gulp as my front-end build tool.

I used [cssmin](https://www.npmjs.com/package/gulp-cssmin) as my CSS minify tool.

By default it can extreme compress CSS file.

The one problem happen!

![螢幕快照 2016-08-31 下午4.07.02.png](http://user-image.logdown.io/user/3170/blog/3202/post/824645/XoWnChm1TTqJGipwNfkQ_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202016-08-31%20%E4%B8%8B%E5%8D%884.07.02.png)

`display` not match

Because use CSS minify can remove inherited CSS property.

So in webkit browser doesn't has `display: -webkit-flex;` and layout will be an error.

But this is not a bug, it is a feature.

It can avoid inherited CSS property and it can decrease CSS file size.

But in this case, it is not good feature.

So i need add option in my gulp file.

```javascript
cssmin({
    aggressiveMerging: false
})
```

It represent to aggressive merging of CSS properties.
