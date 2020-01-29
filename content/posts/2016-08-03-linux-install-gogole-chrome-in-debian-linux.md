---
layout: post
title: 'Linux - install gogole chrome in debian Linux'
date: 2016-08-03
comments: true
categories: [linux, chrome]
---
## Linux - install gogole chrome in debian Linux

```shell
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -

sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'

sudo apt-get update

sudo apt-get install google-chrome-stable
```

[refer - How to install Chrome browser properly via command line?](http://askubuntu.com/questions/79280/how-to-install-chrome-browser-properly-via-command-line)
