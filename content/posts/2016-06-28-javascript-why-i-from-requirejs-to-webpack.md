---
layout: post
title: 'JavaScript - Why i from RequireJS to webpack'
date: 2016-06-28
comments: true
categories: [JavaScript webpack RequireJS]
---
## Why i from RequireJS to webpack

[RequireJS](http://requirejs.org/) is a Asynchronous Module Definition(AMD) lib

Its powerful to handle modulize on your page and you can handle all loader on JavaScript, you can focus on JavaScript function and web page.

But if your module is become complex and more module, you can find JavaScript request become more and more.

You can find it is a serious performance problem.

Your network has lot of request of js.

I want to less or one js request on a page

So i choice [webpack](http://webpack.github.io/docs/) this tool.

It's powerfull tool handle module bundle.

This is what i want change.

Before

![requirejs.png](http://user-image.logdown.io/user/3170/blog/3202/post/745512/GJSJQZt7Si2hu2CVLE3g_requirejs.png)

After

![webpack.png](http://user-image.logdown.io/user/3170/blog/3202/post/745512/rVQY4FhgRO6ctsPQZwPP_webpack.png)

If want to use a lib for global like jQuery

Must use npm install & use ProvidePlugin in `webpack.config.js`

```javascript
...
plugins: [
    new webpack.ProvidePlugin({
        $: "jquery",
        jQuery: "jquery",
        "window.jQuery": "jquery"
    }),
],
...
```

### How it run

You can use

```
webpack
# if you want watch change
webpack --watch
```

more in [https://webpack.github.io/docs/cli.html](https://webpack.github.io/docs/cli.html)

### Use case

If you want bundle all file in directory

```javascript
var fs = require('fs'),
    entries = fs.readdirSync('./mobile/js/').filter(function(file) {
        return file.match(/.*\.js$/);
    });
```

`entries` is a Array show all file.

### My webpack

<script src="https://gist.github.com/tedshd/614ee6f36a6ec6b76ffb088482ef7ba8.js"></script>
