---
layout: post
title: 'youtube-dl - 使用筆記'
date: 2019-11-04
comments: true
categories: [youtube]
---
## youtube-dl - 使用筆記

[youtube-dl](https://ytdl-org.github.io/youtube-dl/index.html) 是一個跟影音相關方便使用的 cli 工具

這裡筆記一下一些用法

列出該影片可以下載的 format

```shell
youtube-dl -F <URL>
```

output

```shell
[youtube] e17Um7wExuQ: Downloading webpage
[youtube] e17Um7wExuQ: Downloading video info webpage
[info] Available formats for e17Um7wExuQ:
format code  extension  resolution note
249          webm       audio only tiny   54k , opus @ 50k (48000Hz), 192.69KiB
250          webm       audio only tiny   72k , opus @ 70k (48000Hz), 255.58KiB
140          m4a        audio only tiny  130k , m4a_dash container, mp4a.40.2@128k (44100Hz), 476.29KiB
251          webm       audio only tiny  138k , opus @160k (48000Hz), 500.94KiB
278          webm       82x144     144p   32k , webm container, vp9, 30fps, video only, 105.14KiB
160          mp4        82x144     144p   43k , avc1.4d400b, 30fps, video only, 147.87KiB
242          webm       136x240    144p   72k , vp9, 30fps, video only, 224.00KiB
133          mp4        136x240    144p   90k , avc1.4d400c, 30fps, video only, 303.08KiB
243          webm       202x360    240p  130k , vp9, 30fps, video only, 379.65KiB
134          mp4        202x360    240p  219k , avc1.4d400d, 30fps, video only, 659.67KiB
244          webm       270x480    240p  235k , vp9, 30fps, video only, 670.44KiB
135          mp4        270x480    240p  375k , avc1.4d4015, 30fps, video only, 1.10MiB
247          webm       406x720    360p  428k , vp9, 30fps, video only, 1.19MiB
248          webm       608x1080   480p  737k , vp9, 30fps, video only, 2.03MiB
136          mp4        406x720    360p  761k , avc1.4d401e, 30fps, video only, 2.09MiB
137          mp4        608x1080   480p 1458k , avc1.64001f, 30fps, video only, 3.95MiB
271          webm       810x1440   720p 2767k , vp9, 30fps, video only, 6.69MiB
313          webm       1080x1920  1080p 4410k , vp9, 30fps, video only, 12.22MiB
43           webm       640x360    360p , vp8.0, vorbis@128k, 1.28MiB
18           mp4        202x360    240p  359k , avc1.42001E, mp4a.40.2@ 96k (44100Hz), 1.29MiB
22           mp4        406x720    360p  713k , avc1.64001F, mp4a.40.2@192k (44100Hz) (best)
```

下載指定的 format

```shell
youtube-dl -f <format code> <URL>
```

下載最好的

```shell
youtube-dl -f best <URL>
```

下載指定的 format

```shell
youtube-dl -f mp4 <URL>
```
