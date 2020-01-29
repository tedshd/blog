---
layout: post
title: 'Golang - gvm Golang version manger'
date: 2019-06-14
comments: true
categories: [golang]
---
## gvm

### Intro

[gvm](https://github.com/moovweb/gvm)

Golang version manger

### Usage

1. Install
```shell
bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
```

2. Add to .bashrc or .zshrc
```shell
# added gvm command to shell
source "$HOME/.gvm/scripts/gvm"
# directory path for GO
export GOPATH=$HOME/gopath
export GOROOT=$HOME/go
export PATH=$PATH:$GOROOT/bin
```

3. Install go
```shell
gvm install go1.4 -B
gvm use go1.4
export GOROOT_BOOTSTRAP=$GOROOT
gvm install go1.9
```

4. Finall add command to .bashrc or .zshrc
```shell
gvm use go1.9
```

[Refer - Go - 在 OSX 安裝 GVM](https://codingluka.com/gvm-in-osx/)
