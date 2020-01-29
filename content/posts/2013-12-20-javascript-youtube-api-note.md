---
layout: post
title: 'JavaScript - YouTube API note'
date: 2013-12-20
comments: true
categories: [javascript, YouTube, google]
---
## JavaScript - YouTube API note

[player demo](https://developers.google.com/youtube/youtube_player_demo)
[YouTube JavaScript Player API Reference](https://developers.google.com/youtube/js_api_reference)
[YouTube 嵌入式播放器参数](https://developers.google.com/youtube/player_parameters?playerVersion=HTML5&hl=zh-cn)
[YouTube Embedded Players and Player Parameters](https://developers.google.com/youtube/player_parameters?hl=en)
[YouTube Player API Reference for iframe Embeds](https://developers.google.com/youtube/iframe_api_reference)

Use YouTube video must init a youtube player
There have 2 player we can use

* flash player
* **iframe player**

I suggest use iframe player because it can support flash and HTML5
If use Apple mobile devices, they can't support flash
Use iframe player can solve this problem
We can use javascript control player

### This is a note to iframe API

embed script

```html
<script src="https://www.youtube.com/iframe_api"></script>
```

JavaScript generate

```javascript
var tag = document.createElement('script'),
    firstScriptTag = document.getElementsByTagName('script')[0];
tag.src = 'https://www.youtube.com/iframe_api';
firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
```

1.First check load iframe API

```javascript
function onYouTubeIframeAPIReady() {
    // do something
}
```

2.Init YouTube player

```javascript
var player;
player = new YT.Player(
    'player',
    {
        width: '1280', // player width
        height: '720', // player height
        videoId: videoList[0], // youtube id ex: '0lfDNu-k6oo'
        playerVars: {
            rel: 1,
            autoplay: 0,
            disablekb: 0,
            showsearch: 0,
            showinfo: 0,
            controls: 1,
            wmode: 'opaque',
            hd: 1,
            html5: 1,
            iv_load_policy: 3
        },
        events: {
            'onReady'        : onPlayerReady,
            'onStateChange'  : onPlayerStateChange,
            'onError'        : error
        }
    }
);
```
playerVars can refer [YouTube 嵌入式播放器参数](https://developers.google.com/youtube/player_parameters?playerVersion=HTML5&hl=zh-cn)

3.Handle onPlayerReady, onPlayerStateChange, error

```javascript
function onPlayerReady(e) {
    // do something
}

function onPlayerStateChange(e) {
    // do something
}

function error(e) {
    // do something
}
```

### Sample code

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>youtube_iframe_api</title>
</head>
<body>
    <div id="player"></div>
</body>
<script>
    var player;

    function loadPlayer() {
        if (document.querySelector('#player')) {
            // get API
            var tag = document.createElement('script'),
            firstScriptTag = document.getElementsByTagName('script')[0];
            tag.src = 'https://www.youtube.com/iframe_api';
            firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

            var videoList = [],
                playCount = 0;

            var video_ID = {
                'v_2': 'V8BTsiMxyaQ',
                'v_0': '7wvNwOPprBE',
                'v_1': 'mTSuiGubCHE',
                'v_8': 'DDs5bXh4erM',
                'v_3': 'n-BXNXvTvV4',
                'v_4': 'CRJDQQXS4uE',
                'v_5': 'ASO_zypdnsQ',
                'v_6': 'IZkYdqRWKaY',
                'v_7': '9Y15es8OY0U',
                'v_9': 'LWV-f6dMN3Q'
            };

            // videoList array
            for(var key in video_ID) {
                var value = video_ID[key];
                videoList.push(value);
            }

            function playChannel() {
                // init player
                player = new YT.Player(
                    'player',
                    {
                        width: '1280',
                        height: '720',
                        videoId: videoList[0],
                        playerVars: {
                            rel: 1,
                            autoplay: 1,
                            disablekb: 0,
                            showsearch: 0,
                            showinfo: 0,
                            controls: 1,
                            autohide: 0,
                            modestbranding: 0,
                            wmode: 'opaque',
                            hd: 1,
                            html5: 1,
                            iv_load_policy: 3
                        },
                        events: {
                            'onReady'        : onPlayerReady,
                            'onStateChange'  : onPlayerStateChange,
                            'onError'        : error
                        }
                    }
                );

                // play video
                function onPlayerReady(e) {
                    console.log('onPlayerReady');
                }

                function error(e) {
                    console.log('Error');
                    console.log(e);
                }
            }

            function onPlayerStateChange(e) {
                // get state
                console.log(e);

                // play list loop when video end play next video
                if (e.data === 0) {
                    playCount++;
                    if (playCount > (videoList.length -1)) {
                        playCount = 0;
                    }
                    player.loadVideoById(videoList[playCount]);
                    player.playVideo();

                }
            }

            function onYouTubeIframeAPIReady() {
                playChannel();
            }

            setTimeout(function() {
                onYouTubeIframeAPIReady();
            }, 1200);
        }
    }

    loadPlayer();
</script>
</html>
```

[Refer - Force HTML5 youtube video](http://stackoverflow.com/questions/5845484/force-html5-youtube-video)

### onError error code

* 2 – The request contains an invalid parameter value. For example, this error occurs if you specify a video ID that does not have 11 characters, or if the video ID contains invalid characters, such as exclamation points or asterisks.
* 5 – The requested content cannot be played in an HTML5 player or another error related to the HTML5 player has occurred.
* 100 – The video requested was not found. This error occurs when a video has been removed (for any reason) or has been marked as private.
* 101 – The owner of the requested video does not allow it to be played in embedded players.
* 150 – This error is the same as 101. It's just a 101 error in disguise!

### Youtube Data api

Get video data api
```
http://gdata.youtube.com/feeds/api/videos/<youtube_id>
```
It return format is XML
```
http://gdata.youtube.com/feeds/api/videos/<youtube_id>?alt=json
```
It return format is json

[参考指南：Data API 协议](https://developers.google.com/youtube/reference?hl=zh-cn)
[Developer's Guide: JSON / JavaScript](https://developers.google.com/youtube/2.0/developers_guide_json?hl=zh-cn)
[Refer- How to ensure YouTube API only returns videos that are streamable on iPhone?](http://stackoverflow.com/questions/2601193/how-to-ensure-youtube-api-only-returns-videos-that-are-streamable-on-iphone)

### Something note

Player API 其中有個參數允許強制使用 HTML5 player 這建議有個好處與壞處
好處是不會有廣告
壞處是如果遇到訊源只有 flash 格式的影片 player 會重啟為 flash player
用 gData 抓影片資訊可抓到其中一個 ```content``` 的 key 其中就有提供此影片所帶有的格式
[test page](http://tedshd.lionfree.net/demo/youtube_api/youtube_video_gdata.html)

* 5 - HTTP URL to the embeddable player (SWF) for this video. This format is not available for a video that is not embeddable. Developers commonly add &format=5 to their queries to restrict results to videos that can be embedded on their sites.
* 1 - RTSP streaming URL for mobile video playback. H.263 video (up to 176x144) and AMR audio.
* 6 - RTSP streaming URL for mobile video playback. MPEG-4 SP video (up to 176x144) and AAC audio.

[Refer - Reference Guide: Data API Protocol](https://developers.google.com/youtube/2.0/reference?hl=zh-tw#Custom_parameters)

實測在 mobile 裝置上(Android, iOS), 參數設定 autoplay 是無效的, 利用 JavaScript 控制讓 youtube 播放也是無效的, 必須用手去點擊播放
