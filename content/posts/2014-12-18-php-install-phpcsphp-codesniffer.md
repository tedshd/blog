---
layout: post
title: 'PHP - install phpcs(PHP CodeSniffer)'
date: 2014-12-18
comments: true
categories: [php]
---
## PHP - install phpcs(PHP CodeSniffer)

Use pear install phpcs

### in Linux(Ubuntu 14.04)

```shell
sudo pear install --alldeps php_codesniffer
```

### in Mac(Mac OS X 10.10.1 Yosemite)

#### install pear

```shell
sudo curl -O  http://pear.php.net/go-pear.phar
```

then

```shell
sudo php -d detect_unicode=0 go-pear.phar
```

Update

```shell
pear upgrade pear
```

```shell
pear upgrade
```

#### install codesniffer

```shell
sudo pear install --alldeps php_codesniffer
```

check

```shell
phpcs -i
```

return

```shell
The installed coding standards are MySource, PEAR, PHPCS, PSR1, PSR2, Squiz and Zend
```

if return

```shell
Warning: include_once(PHP/CodeSniffer/CLI.php): failed to open stream: No such file or directory in /usr/bin/phpcs on line 22

Warning: include_once(): Failed opening 'PHP/CodeSniffer/CLI.php' for inclusion (include_path='.:') in /usr/bin/phpcs on line 22

Fatal error: Class 'PHP_CodeSniffer_CLI' not found in /usr/bin/phpcs on line 25
```

Must include pear path

Modify php.ini

```shell
sudo vim /etc/php.ini
```

```ini
include_path = ".:/usr/share/pear"
```

### Usage

```shell
phpcs <php file>
```

[Refer - PEAR - PHP Extension and Application Repository](http://pear.php.net/)
[Refer - PHP_CodeSniffer](http://pear.php.net/package/PHP_CodeSniffer/download)
[Refer - Code Sniffer](https://rtcamp.com/tutorials/standards/php/code-sniffer/)
[Refer - Installing PEAR on OSX 10.9 Mavericks and OSX10.8/10.7](http://coolestguidesontheplanet.com/installing-pear-osx-10-9-mavericks-osx10-810-7/)
