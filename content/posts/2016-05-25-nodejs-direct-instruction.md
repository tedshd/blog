---
layout: post
title: 'Node.js - 直接執行指令'
date: 2016-05-25
comments: true
categories: [nodejs]
---
## Node.js - 直接執行指令

因為最近要用 nodejs 做一些事, 所以就趕鴨子上架的先把功能做出來再說

然後就立馬遇到問題了...

在 PHP 中要直接執行 command line 是使用 `exec`

因為之前都用 PHP 寫 Shell Scripts 所以找了一下用 nodejs 要如何寫

先是找到了以下的 code

```javascript
function run_cmd(cmd, args, callBack ) {
    var spawn = require('child_process').spawn;
    var child = spawn(cmd, args);
    var resp = "";

    child.stdout.on('data', function (buffer) { resp += buffer.toString(); });
    child.stdout.on('end', function() { callBack (resp); });
}

// example
run_cmd( "ls", ["-l"], function(text) {
    console.log (text) ;
});
```

但是發現如果是要用像是 `mkdir` 或者要 run shell 就會出 `ENOENT` 的 error

結果找到了其他的範例程式碼改良後

```javascript
function exec_cmd(cmd, callBack ) {
    var childProcess = require('child_process');

    var ls = childProcess.exec(cmd, function (error, stdout, stderr) {
        if (error) {
            console.log(error.stack);
            console.log('Error code: '+error.code);
        }
        console.log('Child Process STDOUT: '+ stdout);
        callBack(stdout);
    });
}
```

這樣就行了

這似乎是因為 `spawn` 和 `exec` 的機制的問題

但查了一下, 還是不了解 `spawn` 和 `exec` 在這例子中的差別與錯誤的發生原因, 只能等有空時再來研究了...

[Refer - Node.js进程通信模块child_process](http://blog.fens.me/nodejs-child-process/)
[Refer - 说说Node.js child_process模块中的spawn和exec方法](http://www.html-js.com/article/A-day-to-learn-to-talk-about-JavaScript-spawn-and-exec-Nodejs-in-the-childprocess-module)
