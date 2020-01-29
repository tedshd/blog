---
layout: post
title: 'file upload show progress bar'
date: 2013-10-06
comments: true
categories: [file_upload, javascript]
---
## file upload show progress bar

If you want show upload progress, you must use AJAX method.
And you upload files use FormData object.
XMLHttpRequest object has upload properties
[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
[nsIXMLHttpRequestEventTarget](https://developer.mozilla.org/en-US/docs/XPCOM_Interface_Reference/nsIXMLHttpRequestEventTarget)

sample code
```javascript
xmlHttpRequest.upload.onprogress = function (e) {
    console.log('onprogress', e);
    console.log(e.loaded);
    // progress
    console.log(Math.ceil((e.loaded/e.total) * 100) + '%');
};
```

[Refer](http://codular.com/javascript-ajax-file-upload-with-progress)
