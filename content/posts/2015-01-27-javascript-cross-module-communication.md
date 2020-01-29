---
layout: post
title: 'JavaScript - Cross Module Communication'
date: 2015-01-27
comments: true
categories: [javascript]
---
## JavaScript - Cross Module Communication

When website modulize, need a better way handle cross module communcation.

Refer JavaScript design pattern's observer pattern and Android EventBus

### Principle

![observer_pattern_basic.png](http://user-image.logdown.io/user/3170/blog/3202/post/252556/8wtWEky0QYqHmnFn4agd_observer_pattern_basic.png)

### My Implement

![observer_pattern_flow.png](http://user-image.logdown.io/user/3170/blog/3202/post/252556/YGA8Jj0Tv6Dco8Kj6AI3_observer_pattern_flow.png)

### Example

![observer_pattern_example.png](http://user-image.logdown.io/user/3170/blog/3202/post/252556/NWYJbTKmUJtIkTXZugbf_observer_pattern_example.png)

Hub is a array put publish object

publish object must include action and something want to do

```javascript
var funcA = function () {
	alert('Red Alarm');
}
publish('alarm', funcA);
```

If more something to in same action

```javascript
var funcA = function () {
	alert('Red Alarm');
}
var funcB = function () {
	console.log('Red Alarm');
}
publish('alarm', funcA);
publish('alarm', funcB);
```

Now fire `alarm` can run `funA` and `funB`
Then unpublish `funA`, action can only run `funB`

```javascript
var funcA = function () {
	alert('Red Alarm');
}
var funcB = function () {
	console.log('Red Alarm');
}
publish('alarm', funcA);
publish('alarm', funcB);
unPublish('alarm', funcA);
```

unPublish has three type

```javascript
unPublish('alarm', funcA);
// or
unPublish('', funcA);
// or
unPublish('alarm');
```

If publish is a is async behavior(AJAX)
fire can add second argument as a callback to handle simple async behavior
But not handle something behavior like promises or watchdog

```javascript
fire('alarm');
// or
function funcA() {
	console.log('Fin');
}
fire('alarm', funcA)
```
