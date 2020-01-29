---
layout: post
title: 'Mac - Use readlink in Mac OS X'
date: 2018-10-24
comments: true
categories: [Linux, Mac]
---
## Mac - Use readlink in Mac OS X

1. install `coreutils`

```shell
brew install coreutils
```

2. test greadlink

```shell
greadlink -f <file name>
```

3. alias command line

```shell
alias readlink=greadlink
```

[refer - How can I get the behavior of GNU's readlink -f on a Mac?](https://stackoverflow.com/questions/1055671/how-can-i-get-the-behavior-of-gnus-readlink-f-on-a-mac);
