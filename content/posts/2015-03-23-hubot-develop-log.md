---
layout: post
title: 'Hubot - Develop log'
date: 2015-03-23
comments: true
categories:
---
## Hubot - Develop log

[HUBOT](https://hubot.github.com/)

### Develop Environment

* Mac OS X

### Require

* nodejs(install from brew)
* redis(install from brew)

### install

```shell
npm install -g yo generator-hubot
```

製作資料夾

```shell
mkdir myhubot
cd myhubot
```

設定 hubot

```shell
yo hubot
```

```shell
? Owner: <bot owner>
? Bot name: <bot name>
? Description: <description about this bot>
? Bot adapter: <campfire or shell>
```

資訊會放在 `package.json`

[Refer - Getting Started](https://hubot.github.com/docs/)

### Use it
