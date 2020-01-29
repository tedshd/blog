---
layout: post
title: 'Website switch layout'
date: 2013-12-08
comments: true
categories: [css, javascript]
---
## Website switch layout

之前看過不少網站有切換 layout 的功能
於是就試著做做看

[Demo](http://tedshd.lionfree.net/demo/resume/resume.html)

主要利用定義在 ```body``` 上的 class 去做不同 layout 的切換

Sample code

```javascript
var node;
function node(selector) {
    return document.querySelector(selector);
}

// set style
var layoutList = 'layoutList',
    layoutGrid = 'layoutGrid',
    layoutFull = 'layoutFull',
    layoutCard = 'layoutCard';

function changeLayout(style) {
    // maybe make loading?
    node('body').setAttribute('class', style);
}

// bind click change style
node('#style_1').addEventListener('click', function () {
    changeLayout(layoutGrid);
});
node('#style_2').addEventListener('click', function () {
    changeLayout(layoutList);
});
node('#style_3').addEventListener('click', function () {
    changeLayout(layoutCard);
});
node('#style_4').addEventListener('click', function () {
    changeLayout(layoutFull);
});

/*
scss example

.layoutList {
    .bd {
        .con {
            color: #ff0000;
        }
    }
}
.layoutGrid {
    .bd {
        .con {
            color: #0088ff;
        }
    }
}
.layoutFull {
    .bd {
        .con {
            color: #ff8800;
        }
    }
}
.layoutCard {
    .bd {
        .con {
            color: #00ff00;
        }
    }
}
 */
```
