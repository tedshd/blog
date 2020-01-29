---
layout: post
title: 'performance-test'
date: 2013-08-03
comments: true
categories: [javascript]
---
## performance
jsPerf — JavaScript performance playground
http://jsperf.com/

HTML5 test
http://html5test.com/

JavaScript Benchmark
http://www.webkit.org/perf/sunspider/sunspider.html

```javascript
var perf = function (testName, fn) {
    var startTime = new Date().getTime();
    fn();
    var endTime = new Date().getTime();
    console.log(testName + ": " + (endTime - startTime) + "ms");
}
```
```javascript
jQuery
console.time("timerName");
// javascript
console.timeEnd("timerName");
```
