---
layout: post
title: 'file upload using ajax'
date: 2013-09-29
comments: true
categories: [file_upload, javascript]
---
## File upload using ajax

Use [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData) objects
[Using FormData Objects](https://developer.mozilla.org/en-US/docs/Web/Guide/Using_FormData_Objects)

FormData object only IE 10 up
if IE use ajax upload, only use iframe method.

### sample

**HTML**
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>upload_AJAX</title>
</head>
<body>
    <form action="upload_one.php" method="post" enctype="multipart/form-data">
        <label for="file">File:</label>
        <input type="file" name="Upfile" id="select"><br>
        <input type="submit">
    </form>
    <a href="javascript:upload()">AJAX_upload</a>
</body>
</html>
```

**JavaScript**
```javascript
function upload () {
    // init FormData object
    var formData = new FormData();
    // use append method append upload file
    formData.append('Upfile', document.getElementById('select').files[0]);
    // init XMLHttpRequest object
    var xmlHttpRequest = new XMLHttpRequest();
    // init to backend
    xmlHttpRequest.open('POST', 'upload_one.php');
    // check ajax status
    xmlHttpRequest.onreadystatechange = function () {
        if (xmlHttpRequest.readyState == 4) {
            if (xmlHttpRequest.status == 200) {
                alert('upload');
            }
        }
    };
    // post to backend
    xmlHttpRequest.send(formData);
}
```
