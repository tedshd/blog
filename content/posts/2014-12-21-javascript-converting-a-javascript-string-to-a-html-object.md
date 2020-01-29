---
layout: post
title: 'JavaScript - Converting a JavaScript string to a html object'
date: 2014-12-21
comments: true
categories: [javascript]
---
## JavaScript - Converting a JavaScript string to a html object

```javascript
var str = '<div id="myDiv"></div>';
var htmlObject = document.createElement('div');
htmlObject.innerHTML = str;
/* htnkObject is obj;
<div>
	<div id="myDiv"></div>
</div>
*/
```

[Refer - converting a javascript string to a html object](http://stackoverflow.com/questions/2522422/converting-a-javascript-string-to-a-html-object)
