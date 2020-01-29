---
layout: post
title: 'gitconfig'
date: 2013-08-23
comments: true
categories: [git]
---
## gitconfig

Mac gitconfig
path
```
~/.gitconfig
```

```sh
[user]
		name = tedshd
		email = tedshd@gmail.com
[alias]
		st = status
		co = checkout
		br = branch
		d = difftool
[color]
		diff = auto
		status = auto
		branch = auto
		ui = auto
[credential]
		helper = osxkeychain
[push]
		default = simple
[core]
		editor = vim
[diff]
		tool = vimdiff
[difftool]
		prompt = false
```

vim diff
```sh
git d
```

terminal
```sh
git diff
```
