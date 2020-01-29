---
layout: post
title: 'jQuery-design pattern'
date: 2013-08-08
comments: true
categories: [jquery]
---
## modulize
* modulize selector
```javascript
var module = $('body');
module.on('click', 'a', function() {
		// dosomething...
});
```
* initialize
```javascript
if ($('body').length) {
		// dosomething
}
```

## selector

id is better than tag and class

HTML
```html
<div>
    <ul>
    	<li id="id" class="class">text</li>
    </ul>
</div>
```

JavaScript
```javascript
$('#id').html();
$('body').find('#id');
```

[jsperf](http://jsperf.com/jquery-getnode-test/2)

##bind event
use on
bind on parent selector
```javascript
$('ul').on('click', 'li', function () {
	// dosomething
});
```

[js Bin](http://jsbin.com/ijovot/1/edit)
