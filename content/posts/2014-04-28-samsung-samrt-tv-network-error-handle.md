---
layout: post
title: 'Samsung Samrt TV - Network Error Handle'
date: 2014-04-28
comments: true
categories: [Samsung]
---
## Samsung Samrt TV - Network Error Handle

### Example

Watch network connect status

1. Add web api in HTML

```html
<script type="text/javascript" language="javascript" src="$MANAGER_WIDGET/Common/webapi/1.0/webapis.js"></script>
```

2. Add JavaScript code

```javascript
var watchCB = {
    onconnect : function (type) {
        // (1) connected
        alert(type + " is connected successfully");
    },

    ondisconnect : function(type) {
        // (0) disconnected
        alert(type + " is disconnected");
    }
};

function successCB(networks) {
    for (var i = 0; networks.length; i++) {
        if (networks[i].isActive()) {
            networks[i].setWatchListener(watchCB, errorCB);
        }
    }
};

function errorCB(error) {
    alert(error.message);
};

try {
    webapis.network.getAvailableNetworks(successCB, errorCB);
} catch (error) {
    document.querySelector('h4').innerHTML = error.name;
    alert(error.name);
}
```

This sample code can detect network connect status

[Refer - Web Device API](http://www.samsungdforum.com/Guide/ref00008/index.html)
[Refer - Network](http://www.samsungdforum.com/Guide/ref00008/network/dtv_network_module.html)
