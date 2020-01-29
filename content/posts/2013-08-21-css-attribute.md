---
layout: post
title: 'CSS attribute'
date: 2013-08-21
comments: true
categories: [css]
---
## CSS attribute

### 顏色與背景
```CSS
color:
background-color:
background-images:
background-repeat: no-repeat repeat-x repeat-y repeat
background-position: center
background-attachment: fixed scroll;
background: url() left center no-repeat;
```

### 文字
```CSS
text-align: left right center
vertical-align: top bottom text-top text-bottom middle baseline super sub
line-height:
letter-spacing: (字距)
word-spacing: (單字間距)
text-indent: (首行縮排)
font-family:
font-size:
font-weight: 100~900
font-style: italic oblique
text-decoration: underline overline line-through none
text-decoration: blink 文字閃爍(部分瀏覽器有用)
text-decoration: line-through 刪除線
text-decoration: overline 文字頂部加線
text-decoration: underline 文字底部加線
text-decoration: none 沒有改變
```

### 區塊
```CSS
margin:
padding:
border-color: transparent
border-width:
border-style: solid double dotted dashed inset outset groove ridge
width:
height:
vertical-align: middle
```

### 編排與顯示
```CSS
float:left right
clear:left right both
position:relative absolute fixed
top:
left:
right:
bottom:
z-index:
display: block inline-block none inline
visibility: hidden visible
overflow: hidden scroll auto
```

### 條列項目
```CSS
list-style: none disc square
```

### 其他
```CSS
cursor: pointer crosshair wait help text move
```

### 虛擬樣式
```CSS
:link 當文字或圖案是連結時
:hover 當滑鼠指標移到連結文字或圖案
:avctive 當滑鼠按下連結文字或圖案
:visited 當連結已經點過時
:focus focus
:before {
	content: "";
}
:after {
	content: "";
}
```
