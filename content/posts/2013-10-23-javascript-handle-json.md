---
layout: post
title: 'JavaScript - handle JSON'
date: 2013-10-23
comments: true
categories: [javascript]
---
## handle JSON

先了解 Object & JSON
[JavaScript 物件導向的寫法](http://www.josephjiang.com/presentation/OOJS/object-oriented-paradigms.html)
[你不可不知的 JSON 基本介紹](http://blog.wu-boy.com/2011/04/%E4%BD%A0%E4%B8%8D%E5%8F%AF%E4%B8%8D%E7%9F%A5%E7%9A%84-json-%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%B4%B9/)

```javascript
// data can get from AJAX or self
var data;
// init from self
// Object Literal
data = {
    "data_01": {
        "title": "title 01",
        "num": 01,
        "con": {
            "con_01": {
                "name": "news",
                "desc": "about news"
            }
            "con_02": {
                "name": "sport",
                "desc": "sport like NBA"
            }
            "con_03": {
                "name": "tech",
                "desc": "3C info"
            }
        }
    },
    "data_02": {
        "title": "title 02",
        "num": 02,
        "con": {
            "con_01": {
                "name": "life",
                "desc": "people's life"
            }
            "con_02": {
                "name": "movie",
                "desc": "Iron man ..."
            }
            "con_03": {
                "name": "cars",
                "desc": "TOYOTA, Ford..."
            }
        }
    }
};
```

### init a new object array
```javascript
var x,
    newData = {},
    newDataArr = [];
for (x in data) {
    if (data.hasOwnProperty(x)) {
        newData = {
            data[x].title,
            data[x].num
        };
        newDataArr.push(newData);
    }
}
```

### get object con
```javascript
var x,
    y,
    desc,
    newDescArr = [],
    newConArr = [];
for (x in data) {
    if (data.hasOwnProperty(x)) {
        for (y in data[x].con) {
            if (data[x].con.hasOwnProperty(y)) {
                desc = data[x].con[y].desc;
                newDescArr.push(desc);
            }
        }
        newConArr.push(newDescArr);
    }
}
```

### search value in Object

```javascript
var data = {
    'bind': 27,
    user: [
        {
            'id': 12,
            'desc': 'str'
        },
        {
            'id': 34,
            'desc': 'hahaha'
        },
        {
            'id': 27,
            'desc': 'hihihi'
        }
    ]
};
var x;
for (x in data.user) {
  if(data.user[x].uid === data.bind) {
    count = x;
  }
}
console.log(data.user[count]);
alert(JSON.stringify(data.user[count]));
```
