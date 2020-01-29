---
layout: post
title: 'miiiTV for Samsung Smart TV'
date: 2014-01-21
comments: true
categories:
---
## miiiTV for Samsung Smart TV

### Time 4~5 week(20 days)

* TV 註冊(app info(partner, brand, model, language, mac) to server get did)
  * brand [TV info](https://www.samsungdforum.com/Guide/ref00008/tvinformation/dtv_tvinformation_module.html)
  * data add url post data
  * sha1 encode[Javascript: Equivalent of PHP's hash_hmac() with RAW BINARY output?](http://stackoverflow.com/questions/12099092/javascript-equivalent-of-phps-hash-hmac-with-raw-binary-output)[CryptoJS 3.1](https://code.google.com/p/crypto-js/#The_Hasher_Output)
* jsonp getChannelList/pid
  * jsonp post {source: tv}
* User 和 TV 綁定(與取消 User)
* TV 取 Channel 列表
* 資料儲存(以檔案的方式儲存)
  * ```4000 videos data read 3s```
  * did + secret code ```appInfo.data```

```JavaScript
appInfo = {
	did: <did>,
  secretCode: <secret code>
}
```

  * 儲存 user data ```uid.data```

```JavaScript
uid = ['<uid 1>', '<uid 2>'];
```

  * 儲存每個 Channel 播放的影片與時間 ```<uid>/channelLog.data```

```JavaScript
channelLog = {
	<pid>: {
		videoCount: 0,
		t: 200
	}
};
```

* server & browser keep connect(polling or long polling)
* error handle
  * app load(network, API server, check reg, check did)
* 處理 channel 為空的情況
### TV UI

* ~~音量 SOD <span style="color:red">(1 day)</span>~~
* 退出 confirm <span style="color:red">(1 day)</span>
* 按鍵控制資訊
* Menu 選台(已有初版，需優化)
* Channel sort by number
* __**數字鍵轉台**__ <span style="color:red">(3 day)</span>
  * 在建立 menu 時在建一個新結構

```JavaScript
var channelsNumber = {
	100: {
		pid: <pid>,
		title: <channel name>
	},
	200: {
		pid: <pid>,
		title: <channel name>
	},
	201: {
		pid: <pid>,
		title: <channel name>
	}
};
```

* 方向鍵選 video (已有初版)
* Video List (已有 prototype) <span style="color:red">(1 day)</span>
* binding page(ping code)

### Server-side

* 過濾影片內容，排除只能 Flash Player 播放的影片
* v2 API：media$content 需要有 1, 5, 6 三種格式

### flow

使用者第一次進入
確認是否註冊

* 沒註冊過

app info(partner, brand, model, lang) to server get did
要 pre-share key
註冊帶 appinfo, re-share key(json format 用 base64)

* 註冊過

```JavaScript
function checkRegistration() {
	if(!reg) {
		// bind app
		checkRegistration();
	} else {
		startApp();
	}
}
checkRegistration();

function startApp() {
	// start do something
  // check did to get default channel
  // get user channel
  // build channel data(menu video number)
  // videoSelect(open update)
  // menuSelect(open update)
  // bind user(get new user channel)
  // load videos(after select channel, number switch channel)
  // load player
}
```

### pin code

TV(sync app) - request(did) -> API server(gen pin code) - response -> TV(show pin code)
TV(polling) - request(polling)(check pin code) -> API server
App(input pin code) - request(pin code) -> API server(check pin code)

#### UI control

0. welcome view

welcomeState: 0

00. load view

1. setting view

settingStatus: 0

2. Menu UI

menuStatus: 0

3. Video list UI

videoListStatus: 0

4. control info UI

infoStatus: 0

5. channel info UI

channelInfo: 0

### key

* red(playlist)

* green(ch_info, control_info)

* yellow(setting view like box)

* blue(menu)

### 20 days

影片快轉與倒轉

在 Video Info 出現：影片播放時間軸，台長大頭貼與名字

多位使用者列表同步與切換

訂閱頻道被台長設為私人頻道的訊息

訂閱頻道被台長刪除的訊息

記住所有頻道最後看的影片與時間

Page 4-8：menu 的最下方多一個 "更多頻道"

Playlist一次移一列

Page 4-9 ：影片格式或直播訊源為 html5 不支援格式，要有額外處理
Page 4-10：目前無法判定頻道內含 html5 不支援格式，待討論替代方案

播放中遇到網路中斷機制

### Bind users

#### API

/tvservice2/device/unbind
'did'
'uid'

/tvservice2/device/getAllProfileInfo
'did'

save current user uid

save last bind user data show in setting

setting userslist sort uew -> old

```JavaScript
usersChannelLists = {
	<uid>: {
  	<channels number>: {
    	pid: '<pid>',
      title: '<channel title>'
    }
  }
	16: {
  	200: {
    	pid: 1324,
      title: 'channel name'
    },
    201: {
    	pid: 1999,
      title: 'name'
    }
  }
  40: {
  	200: {
    	pid: 2003,
      title: 'video title'
    },
    203: {
    	pid: 4032,
      title: 'title name'
    }
  }
}
```

Users data

```JavaScript
Main.users = {
	<uid>: {
  	uid: <uid>,
    name: '<user name>',
    img: '<image url>'
  },
  16: {
  	uid: 16,
    name: 'Ted',
    img: 'image url'
  }
}
```

#### Flow

解除綁定會切回上一個使用者列表的使用者直到沒有使用者成為預設頻道
綁定後 channel list 與 menu 為新綁定的使用者
綁定使用者後維持播原本的 channel, 但頻道上下轉台為新綁定使用者的 channel(第一個 channel 或 最後一個 channel)
設定頁的使用者列表大頭貼與名字為當前使用者的名字與大頭貼
menu 切換 focus 會維持在同樣位置, 但 focus 在最後一個 channel 時, 由 channel 多的 user 切到 channel 少的 user 時會切到最後一個 channel

### 記憶 channel 最後播放的影片和時間

```JavaScript
Main.usersChannelsLog = {
	<uid>: {
  	<pid>: {
  		breakVideo: <youtube hash>,
    	breakTime: <number sec>
    }
  }
}
```
