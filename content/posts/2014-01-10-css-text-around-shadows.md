---
layout: post
title: 'CSS - 文字圍繞陰影'
date: 2014-01-10
comments: true
categories: [css]
---
## CSS - 文字圍繞陰影

### text-shadow

利用 ```text-shadow``` 可達到文字陰影的效果, 但如果要讓陰影圍繞著文字就需要一點技巧了

CSS

```css
h1 {
    text-shadow: #ff0000 1px 2px 3px;
    /*-- 顏色 x位移 y位移 模糊度 --*/
}
```

要達到圍繞的效果, 必須有上、下、左、右、左上、左下、右上、右下, 最少 8 個方向的位移

| 左上 | 上 | 右上 |
|------|------|------|
| 左 | 文字 | 右 |
| 左下 | 下 | 右下 |

```css
h1 {
    text-shadow:
        #ff8800 5px 0 1px,
        #ff8800 -5px 0 1px,
        #ff8800 0 5px 1px,
        #ff8800 0 -5px 1px,
        #ff8800 5px 5px 1px,
        #ff8800 -5px -5px 1px,
        #ff8800 5px -5px 1px,
        #ff8800 -5px 5px 1px;
}
```

#### codepen

<p data-height="268" data-theme-id="2982" data-slug-hash="HxLJB" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/tedshd/pen/HxLJB'>text shadow</a> by Ted (<a href='http://codepen.io/tedshd'>@tedshd</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

此例可看出尚未完美之處(要把位移對得很精確)
text-shadow 為 CSS3 需 IE10 以上才支援
疊太多 shadow 在上面會影響頁面 render
所以此效果儘量少用

### text-stroke

CSS3 的 text-stroke 可完美達成, 但目前只支援 Chrome, Sarfari, Opera

```css
h1 {
	color: black;
	-webkit-text-fill-color: #fff;
	-webkit-text-stroke-width: 1px;
	-webkit-text-stroke-color: #ff8800;
}
```

#### codepen

<p data-height="268" data-theme-id="2982" data-slug-hash="huBoJ" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/tedshd/pen/huBoJ'>text-stroke</a> by Ted (<a href='http://codepen.io/tedshd'>@tedshd</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>


[Refer - Adding Stroke to Web Text](http://css-tricks.com/adding-stroke-to-web-text/)
[Refer - Can I use CSS text-stroke?](http://caniuse.com/text-stroke)
