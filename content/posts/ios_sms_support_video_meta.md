---
title: "在 iOS Messages 呈現帶影片預覽的連結"
date: 2022-07-20T10:02:11+08:00
draft: false
categories: [ios]
---

最近添加了一個小功能要來測試成效

就是因為 PM 有看到一些服務的連結在 iOS Messages 上呈現並非常見的圖片而是影片

PM 說好像是 iOS 15 以上支援(我自己是沒找到相關的資料證明這件事)

不過應該沒支援的話就呈現圖片

查了一下文件, 其實也不難

基本上就是定義 open graph

多定義

```HTML
<meta property="og:video" content="http://www.example.com/sample.mp4" />
<meta property="og:video:type" content="video/mp4" />
<meta property="og:video:width" content="1280" />
<meta property="og:video:height" content="720" />
```

這邊有個要注意的點是

原來是產出 1:1 的影片, 但發現會上下截掉

所以最後採用 16:9 的比例

## demo

<video width="1280" height="720" controls>
  <source src="https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2Fdemo.mp4?alt=media&token=6c6a2dc8-c859-4f8e-a88f-882d1e77addc" type="video/mp4">
  Your browser does not support the video tag.
</video>

[Refer - Best Practices for Link Previews in Messages](https://developer.apple.com/library/archive/technotes/tn2444/_index.html)