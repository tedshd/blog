---
layout: post
title: 'JavaScript - time seconds to hh:mm:ss'
date: 2014-03-05
comments: true
categories: [javascript]
---
## JavaScript - time seconds to hh:mm:ss


```javascript
function toHHMMSS(sec_num) {
    var hours   = Math.floor(sec_num / 3600);
    var minutes = Math.floor((sec_num - (hours * 3600)) / 60);
    var seconds = Math.floor(sec_num - (hours * 3600) - (minutes * 60));

    if (hours   < 10) {hours   = "0"+hours;}
    if (minutes < 10) {minutes = "0"+minutes;}
    if (seconds < 10) {seconds = "0"+seconds;}
    var time    = hours+':'+minutes+':'+seconds;
    return time;
}

alert(toHHMMSS(1234));
```

[Refer - JavaScript seconds to time with format hh:mm:ss](http://stackoverflow.com/questions/6312993/javascript-seconds-to-time-with-format-hhmmss)
