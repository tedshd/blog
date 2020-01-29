---
layout: post
title: 'javascript - file upload'
date: 2013-10-20
comments: true
categories: [file_upload, javascript]
---
## javascript - file upload

### Introduction

利用 javascript 達到檔案上傳的功能

* 顯示上傳進度
* 多檔上傳
* 取消上傳
* 拖拉上傳
* **[斷點續傳??](http://www.resumablejs.com/)**
* chrome 上傳資料夾
* 盡可能跨 browser(for IE8)
* 不依攋任一 javascript library
* [自幹上傳](http://www.dotblogs.com.tw/anfernee/archive/2011/08/25/34299.aspx)
* [iframe upload in IE](http://viralpatel.net/blogs/ajax-style-file-uploading-using-hidden-iframe/)

### Skill

* files API
* AJAX
* iframe
* FormData
* ...

### Develop

* 單純用 javascript
* 利用 AJAX 上傳
* 處理 AJAX 上傳在 IE 的問題(利用 iframe 也許可解, [Refer](http://malsup.com/jquery/form/))
* 處理拖拉
* 處理拖拉資料夾
* 處理預設樣式

### Issue

* [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData)
  * AJAX 上傳(IE10 以上)
  * IE 利用 iframe 實作

### Dseign flow

#### Attribute

* inputFileNode(input type file element)
* fileName(```name=""```)
* server(the file upload to server url)
* dropArea(set the drop area)

#### Method

* upload
* _cancel_

#### Event

Use [CustomEvent](https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent) (IE 9 up)
[Refer - How to Create Custom Events in JavaScript](http://www.sitepoint.com/javascript-custom-events/)

* selectFiles
  * e.fileList (Array)
      * name
      * size
      * type
  * e.length (number)
* _uploadError_
* uploadProgress
  * e.bytesLoaded (number)
  * e.bytesTotal (number)
  * e.percentLoaded (number)
* _uploadComplete_
* _dragenter_
* _dragover_
* _drop_
* _drag_

### develop log

#### How to do?

Use JavaScript no require any library
Use AJAX to upload
Must know how to use XMLHttpRequest and use it upload file
Use FormData handle ajax upload files, but it only for IE 10
So IE maybe use iframe upload
Must easy to use
It has many useful method and event
Must handle custom event(have cross browser problem)
Use File API handle file list, it only for IE10

#### About code

Use querySelector replace getElementById、getElementsByTagName...etc(IE8 up)
[document.querySelector](https://developer.mozilla.org/en-US/docs/Web/API/document.querySelector)
Use node method to reduce code
```JavaScript
var node;
function node (selector) {
    return document.querySelector(selector);
};

// use
node('#id'); // html id
node('.class'); // html class
node('div'); // html element
```

for IE get upload file name
```JavaScript
var fileName = document.querySelector('#uploadfile').value.match(/[^\/\\]+$/);
```

[Refer - PHP Error Messages Explained](http://php.net/manual/en/features.file-upload.errors.php)
