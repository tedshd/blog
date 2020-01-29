---
layout: post
title: 'CSS - Modify Pseudo Element Content'
date: 2015-04-05
comments: true
categories: [css]
---
## CSS - Modify Pseudo Element Content

之前遇到個問題就是偽元素的內容(content)到底可不可以修改, 於是就求助於 Google

最後的答案是可以的, 而且還不少方法

[Refer - Modify pseudo element styles with JavaScript](http://pankajparashar.com/posts/modify-pseudo-elements-css/)

看下來就以下的方式個人覺得最好用

```css
#red::before {
    content: attr(data-attr);
    color: red;
}
```

```html
<p id="red" data-attr="red">Hi, this is plain-old, sad-looking paragraph tag.</p>
```

```javascript
    setTimeout(function (argument) {
        document.querySelector('#red').setAttribute('data-attr', 'green');
    }, 3000);
```
