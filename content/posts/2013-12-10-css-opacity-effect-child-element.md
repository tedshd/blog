---
layout: post
title: 'CSS - Opacity effect child element'
date: 2013-12-10
comments: true
categories: [css]
---
## CSS - Opacity effect child element

在利用 ```opacity``` 做背景時常遇到個問題就是子元素也被設置 opacity
這時就可以利用 CSS 的 ```:before``` 或 ```:after```

```html
<div class="bg-2">
  <h2>Title</h2>
  <p>Content</p>
  <img src="http://blog.soonr.com/wp-content/uploads/2013/03/Google-Play-Badge.png" alt="google play" />
</div>
```

```css
.bg-2 {
  position: relative;
  &:before {
    content: "";
    z-index: -99;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: #000;
    @include opacity(0.8);
  }
}
```

CodePen

<p data-height="812" data-theme-id="0" data-slug-hash="qeojf" data-user="tedshd" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/tedshd/pen/qeojf'>qeojf</a> by Ted (<a href='http://codepen.io/tedshd'>@tedshd</a>) on <a href='http://codepen.io'>CodePen</a></p>
<script async src="//codepen.io/assets/embed/ei.js"></script>
