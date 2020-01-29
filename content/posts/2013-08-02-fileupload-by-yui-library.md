---
layout: post
title: 'fileUpload by yui library'
date: 2013-08-02
comments: true
categories: [file_upload]
---
## fileUpload by yui library

### init upload button
JavaScript bind click event
in IE
use JavaScript move CSS position

* uploader    : Upload file
* uploaderOut : handle not drag area

### event
---
#### fileSelect
select file & render upload list
check file status
handle fileList
_upload

#### uploadprogress
upload file progress

#### uploadcomplete
upload complete
check ok or fail
_upload

#### uploaderror
cancel & upload next

#### _upload
check file status & upload status
upload
upload fileList[uploadfile]

#### _cancelUpload

### Notice
---
#### Y.Uploader.TYPE
* none(no flash)
* html5
    * drag & drop
* flash(IE)

```javascript
    if (Y.Uploader.TYPE === 'none') {
        console.log('no install flash player');
        return;
    }
    // init upload button
    if (Y.Uploader.TYPE === 'html5') {
        // do something like drag & drop
    } else if (Y.Uploader.TYPE === 'flash') {
        // do something
    }
```

#### Free Space
check free space & show message
update free space

#### Drag & drop
only chrome can check isFile or isDirectory
drop area check(use setTimeOut & clearTimeout)

#### handle UI
when something behavior happen need check UI
like cancel, complete and error

#### upload list control
need update upload list status
like cancel, complete and error
control fileList

#### queue
It is easy to control upload only one file upload and other queue

#### If has total progress
need control  & update total when something behavior happen
like cancel, error and upload more
