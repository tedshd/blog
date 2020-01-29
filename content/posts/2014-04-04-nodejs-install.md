---
layout: post
title: 'Node.js - install'
date: 2014-04-04
comments: true
categories: [javascript, mac, Node.js]
---
## Node.js - install

### Mac

利用 homebrew 安裝

```shell
brew install node
```

[node.js](http://nodejs.org/)
[Refer - Install Node.js and npm using Homebrew on OS X](http://thechangelog.com/install-node-js-with-homebrew-on-os-x/)

### Ubuntu

```shell
sudo apt-get install nodejs-legacy

sudo apt-get install npm
```

[Refer - Can not install packages using node package manager in Ubuntu](http://stackoverflow.com/questions/21168141/can-not-install-packages-using-node-package-manager-in-ubuntu)

### Update

Now node merge iojs and version update to v4

But now homebrew not updgrade to v4

So i use nvm

[Refer - Node.js 安裝與版本切換教學 (for MAC)](http://icarus4.logdown.com/posts/175092-nodejs-installation-guide)

### npm upgrade node version

```shell
sudo npm cache clean -f
sudo npm install -g n
sudo n stable
```

[Refer - Upgrade Node.js via NPM](http://davidwalsh.name/upgrade-nodejs)
