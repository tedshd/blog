---
layout: post
title: 'JavaScript - Google Closure Compiler V.S. Gulp uglify'
date: 2015-08-15
comments: true
categories: [javascript, gulp, uglifyjs, google]
---
## JavaScript - Google Closure Compiler V.S. Gulp uglify

### Intro

I have two choice

1. Google Closure Compiler

2. UglifyJs

#### Google Closure Compiler

[Google Closure Compiler](https://developers.google.com/closure/compiler/)

*Google Closure Compiler* is a tool for minify and uglify js.

* From Google

* Java

* Command Line

* Slow

#### UglifyJs

[mishoo/UglifyJS2](https://github.com/mishoo/UglifyJS2)

* More option setting

* Node.js

* Command Line

* Fast

### Test

#### Google Closure Compiler

When i run command line, it used lot of cpu source.

Can feel it lock some seconds.

If compiler error,it can show error message.

#### UglifyJs

It's so fast.

It can fix some small error when it compiler.

So i recommendation this tool.


Finally i use [Gulp](http://gulpjs.com/) handle uglifyJs.
