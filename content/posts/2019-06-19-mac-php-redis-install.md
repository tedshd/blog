---
layout: post
title: 'Mac - php redis install'
date: 2019-06-19
comments: true
categories: [php, redis]
---
## Mac - php redis install

### Mac Env

Mac OSX 10.14.5

### Step

```shell
git clone https://www.github.com/phpredis/phpredis.git

cd phpredis

phpize && ./configure && make && sudo make install
```

**test**

```shell
php -r "if (new Redis() == true){ echo \"\r\n OK \r\n\"; }"
```

### Troubleshooting

#### phpize

1.

```shell
$ phpize
grep: /usr/include/php/main/php.h: No such file or directory
grep: /usr/include/php/Zend/zend_modules.h: No such file or directory
grep: /usr/include/php/Zend/zend_extensions.h: No such file or directory
Configuring for:
PHP Api Version:
Zend Module Api No:
Zend Extension Api No:
```

**Solution**

```shell
cd /Library/Developer/CommandLineTools/Packages/

open macOS_SDK_headers_for_macOS_10.14.pkg
```

2.

```shell
$ phpize
Cannot find autoconf. Please check your autoconf installation and the $PHP_AUTOCONF environment variable. Then, rerun this script.
```

**Solution**

```shell
brew install autoconf
```


[Refer - install-phpredis-mac-osx](https://stackoverflow.com/questions/51908004/install-phpredis-mac-osx)

[Refer - macOS 10.14软件编译时找不到头文件的解决方法](https://zhile.io/2018/09/26/macOS-10.14-install-sdk-headers.html)

[Refer - macOS 中使用 phpize 动态添加 PHP 扩展的错误解决方法](http://www.mayanlong.com/archives/2016/349.html)
