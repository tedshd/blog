---
layout: post
title: 'file upload 123'
date: 2013-08-20
comments: true
categories: [file_upload]
---
# File Upload

## Server side setting

### php.ini
in Mac
```sh
/etc/php.ini
```
```ini
file_uploads = On
upload_max_filesize = 10M
post_max_size = 10M

file_uploads
# 預設為on,允許用HTTP協定上傳
upload_tmp_dir
# 上傳檔案暫存目錄,wamp5中,c:/wamp/tmp
upload_max_filesize
# 上傳檔案最大值
post_max_size
# 利用 post 傳送數據所用最大值(利用 AJAX 或 post 上傳會有影響)
max_execution_time
# PHP執行時間最大值,預設為30秒
```


## style
由於預設的 ```<input type="file">``` 樣式不好改，且每一個 broswer 預設的樣式都不一樣，所以都會希望用統一化的客制化樣式，但基本上不太可能把它的樣式改成所想要的客制化的樣式，除非直接用像 Bootstrap 之類的框架

### solution 1(hack)
把 ```<input type="file">``` 的 style 設成 opacity: 0; 蓋在客制化的 button 上，也必須要設成跟客制化寬高一樣，以免覆蓋面積不一樣

* CSS
```css
.btn, .file-select {
		width: 80px;
		height: 30px;
}
.btn {
		border: solid 2px #0044ff;
		background: #0088ff;
		color: #ff8800;
		border-radius: 5px;
		text-align: center;
}
.file-select {
		position: relative;
		left: -84px;
		opacity: 0;
}
```

* HTML
```html
<div>
		<button class="btn">Button</button>
		<input type="file" class="file-select">
</div>
```

### solution 2(better)
利用 ```<label></label>``` 的 for 特性來處理
Bootstrap 就是利用這個方法
[demo](http://tedshd.lionfree.net/demo/php/file_style.html)

* HTML
```html
<form action="upload_img.php" method='post' enctype='multipart/form-data'>
    <label for="file-style">
        <input type="button" class="btn" value="Select file">
        <!--if IE, only IE9 up-->
    </label>
    <input type="file" name="file" id="file-style">
    <label for="file-style_2" class="btn btn-primary">
        <span>Select file</span>
    </label>
    <input type="file" name="file_2" id="file-style_2">
    <input type="submit" class="btn btn-primary">
</form>
```

* CSS
```css
/*--把 input 藏起來--*/
#file-style {
		opacity: 0;
		width: 0;
		height: 0;
}
```


點擊 ```<label></label>``` for 會觸發 mapping 到 id 的 ```<input>``` 元素
利用這原理就可以在點擊 ```<label></label>``` 時, 點擊到 ```<input type="file">``` 進而開啓檔案選擇
直接改  ```<label></label>``` 樣式是較好的做法


## Issue

### javascript click input file in IE
由於安全性問題所以在 IE 中利用 javascript 去 click file 做選擇檔案之後，在做 submit 時會發現 IE 會把用 javascript 選的檔案去除，不讓該檔案上傳
[example](http://tedshd.lionfree.net/demo/php/javascript_submit.html)

### upload long name file in IE8/9
在 IE 8/9 中不會讓使用者上傳過長的檔名
直接在 ```<input type="file">``` 那就不會有檔案了
[IE issue](http://social.msdn.microsoft.com/Forums/ie/en-US/b04f2f93-a7aa-4493-94dc-68167077f30b/fileupload-control-fails-to-upload-file-when-file-name-is-255-characters-long)

### if upload image, avoid smaill image or fake picture

### hamdle upload file name like ..jpg or ...docx, ...
