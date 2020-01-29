---
layout: post
title: 'php - Ubuntu 14 PHP 5.6 or to upgrade from PHP 5.5'
date: 2015-10-31
comments: true
categories: [php, ubuntu, Linux]
---
## php - Ubuntu 14 PHP 5.6 or to upgrade from PHP 5.5

```shell
sudo apt-get -y update

sudo add-apt-repository ppa:ondrej/php5-5.6

sudo apt-get -y update

sudo apt-get -y install php5 php5-mhash php5-mcrypt php5-curl php5-cli php5-mysql php5-gd php5-intl php5-xsl php5-bcmath
```

if use `php -v` check version is 5.5.x

I use

```shell
sudo apt-get -u install php5-cli
```

[Refer - PHP 5.5 or 5.6—Ubuntu](http://devdocs.magento.com/guides/v2.0/install-gde/prereq/php-ubuntu.html#instgde-prereq-php56-install-ubuntu)
