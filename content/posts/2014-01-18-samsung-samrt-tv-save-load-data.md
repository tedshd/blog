---
layout: post
title: 'Samsung Samrt TV - save / load data'
date: 2014-01-18
comments: true
categories: [Samsung]
---
## Samsung Samrt TV - save / load data

如果要儲存資料(ex: 使用者資訊...)建議使用 Samsung 的 file API
使用 HTML5 的 localStorage 在電視關機後會被清掉

[File API](http://www.samsungdforum.com/Guide/ref00001/index.html)
[Refer - Can I access a local file from JavaScript code?](http://www.samsungdforum.com/Guide/tec00111/index.html)
[Refer - openCommonFile](http://www.samsungdforum.com/Guide/ref00001/file_api_opencommonfile.html)
[Refer - readAll](http://www.samsungdforum.com/Guide/ref00001/file_api_readall.html)

### example

```javascript

var fileSystemObj = new FileSystem();

function save() {
    if (fileSystemObj.isValidCommonPath(curWidget.id) == 0){
        fileSystemObj.createCommonDir(curWidget.id);
    }
    var fileObj = fileSystemObj.openCommonFile(curWidget.id + '/testFile.data', 'w');
    fileObj.writeAll('test save');
    fileSystemObj.closeCommonFile(fileObj);
}
Main.save = save;

function read() {
    var file = fileSystemObj.openCommonFile(curWidget.id + '/testFile.data', 'r');
    var strResult = file.readAll();
}
Main.read = read;
```
