---
layout: post
title: 'AMP - Accelerated Mobile Pages key point'
date: 2017-08-25
comments: true
categories: [AMP]
---
## Intro

Provide some key point & something we need notice

### 1. meta

In normal page

```html
<link rel="amphtml" href="https://www.example.com/url/to/amp/document.html">
```

In AMP page

```html
<link rel="canonical" href="https://www.example.com/url/to/full/document.html">
```

### 2. Default style(Handle render)

```html
<style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
```

Format

```html
<style amp-boilerplate>
body {
    -webkit-animation: -amp-start 8s steps(1, end) 0s 1 normal both;
    -moz-animation: -amp-start 8s steps(1, end) 0s 1 normal both;
    -ms-animation: -amp-start 8s steps(1, end) 0s 1 normal both;
    animation: -amp-start 8s steps(1, end) 0s 1 normal both
}

@-webkit-keyframes -amp-start {
    from {
        visibility: hidden
    }
    to {
        visibility: visible
    }
}

@-moz-keyframes -amp-start {
    from {
        visibility: hidden
    }
    to {
        visibility: visible
    }
}

@-ms-keyframes -amp-start {
    from {
        visibility: hidden
    }
    to {
        visibility: visible
    }
}

@-o-keyframes -amp-start {
    from {
        visibility: hidden
    }
    to {
        visibility: visible
    }
}

@keyframes -amp-start {
    from {
        visibility: hidden
    }
    to {
        visibility: visible
    }
}
</style>
<noscript>
    <style amp-boilerplate>
    body {
        -webkit-animation: none;
        -moz-animation: none;
        -ms-animation: none;
        animation: none
    }
    </style>
</noscript>
```

### 3. Use `<style amp-custom>` handle style

* only one tag in one page

* Size limit 50k

### 4. GA use `<amp-analytics>` bind by selector

### 5. AJAX CORS

* [CORS Requests in AMP](https://github.com/ampproject/amphtml/blob/master/spec/amp-cors-requests.md)

### 6. form submit use `amp-form`

### 7. absolute link(Must include host name)

### 8. Validate AMP page

* Add `#development=1` on url and open browser develop tool console tab.

* Web tool [validator.ampproject.org](https://validator.ampproject.org)

* Browser extension [Chrome](https://chrome.google.com/webstore/detail/amp-validator/nmoffdblmcmgeicmolmhobpoocbbmknc) or [Opera](https://addons.opera.com/en-gb/extensions/details/amp-validator/)
