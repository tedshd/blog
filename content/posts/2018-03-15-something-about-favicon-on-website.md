---
layout: post
title: 'Something about favicon on website'
date: 2018-03-15
comments: true
categories: [HTML]
---
## Something about favicon on website

Favicon is a icon on browser tab.

But now we must do more thing on mobile device handle favicon.

### 2 way add browser favicon

1. Put icon in url path `<example.com>/favicon.png`

2. Add meta tag `<link rel="icon" type="image/png" href="favicon.png" />`

Notice: I like use png as my favicon, because i can reuse this file.

Icon format case

```HTML
<!-- IE -->
<link rel="shortcut icon" type="image/x-icon" href="favicon.ico" />
<!-- other browsers -->
<link rel="icon" type="image/x-icon" href="favicon.ico" />
```

[Refer - Correct MIME Type for favicon.ico?](https://stackoverflow.com/questions/13827325/correct-mime-type-for-favicon-ico)

## Other icon for web case

For iOS device icon

```html
<link rel="apple-touch-icon" href="<icon url>">
<link rel="apple-touch-icon" sizes="76x76" href="<icon url>">
<link rel="apple-touch-icon" sizes="120x120" href="<icon url>">
<link rel="apple-touch-icon" sizes="152x152" href="<icon url>">
```

For PWA add to home screen

Use manifest.json

[The Web App Manifest | Web Fundamentals | Google Developers](https://developers.google.com/web/fundamentals/web-app-manifest/)
