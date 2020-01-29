---
layout: post
title: 'JavaScript - Random Array Sort'
date: 2014-05-13
comments: true
categories: [javascript]
---
## JavaScript - Random Array Sort


```javascript
function randOrd(){
	return (Math.round(Math.random())-0.5);
}

anyArray = [1, 's', 3, 'arr', 4];
anyArray.sort( randOrd );
alert(anyArray);
```

[Refer - Random Array Sort](http://javascript.about.com/library/blsort2.htm)
