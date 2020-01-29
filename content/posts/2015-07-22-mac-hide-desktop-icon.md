---
layout: post
title: 'Mac - hide desktop icon'
date: 2015-07-22
comments: true
categories: [mac]
---
## Mac - hide desktop icon

### Hide

```shell
defaults write com.apple.finder CreateDesktop -bool false
```

Then

```shell
killall Finder
```

### Show

```shell
defaults write com.apple.finder CreateDesktop -bool true
```

Then

```shell
killall Finder
```

[Refer - Hide All Desktop Icons in Mac OS X](http://osxdaily.com/2009/09/23/hide-all-desktop-icons-in-mac-os-x/)
