---
layout: post
title: 'JavaScript - get text from dom object not include wrap html tag in child'
date: 2016-11-03
comments: true
categories: [JavaScript]
---
## JavaScript - get text from dom object not include wrap html tag in child

### Intro

#### Case 1

```html
<div id="case_1">
	Hi, This is a <em>Apple</em>
</div>
```

I want to get `Hi, This is a `

#### Case 2

```html
<div id="case_2">
	<p>I have a pen.</p>PPAP
</div>
```

I want to get `PPAP`

#### Case 3

```html
<div id="case_3">
	Apple<span> and pen</span> and pineapple pen
</div>
```

I want to get `Apple` and ` and pineapple pen`

Than you can use this

```javascript
function parseText(dom) {
	if (dom.length) {
		console.warn('This is a domlist');
		return;
	}
	var dom = dom.childNodes,
		list = [];
	for(var x = 0;  x< dom.length;x++) {
		if (dom[x].nodeType === 3) {
			var textContent = dom[x].nodeValue,
				matchWrap = textContent.match(/\n +/);
			if (matchWrap) {
				textContent = textContent.replace(matchWrap, '');
			}
			if (textContent) {
				list.push(textContent);
			}
		}
	}
	return list;
}
```

You also can use `filter` handle for loop

[demo](https://tedshd.io/demo/parse_text.html)

[Refer - Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
