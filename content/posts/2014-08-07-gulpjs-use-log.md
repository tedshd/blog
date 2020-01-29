---
layout: post
title: 'gulp.js - Use Log'
date: 2014-08-07
comments: true
categories: [javascript, gulp]
---
## gulp.js - Use Log

### Intro

[gulp.js](http://gulpjs.com/)

[Getting Started](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md#getting-started)

[Grunt vs Gulp - Beyond the Numbers](http://jaysoo.ca/2014/01/27/gruntjs-vs-gulpjs/)

### package.json version setting

[dependencies](https://docs.npmjs.com/files/package.json#dependencies)

### How to pipe to another task in Gulp?

```javascript
gulp.task('first', function() {
   // first task
});

gulp.task('second', ['first'], function() {
   // this occurs after 'first' finishes
});
```

[Refer - How to pipe to another task in Gulp?](http://stackoverflow.com/questions/23458428/how-to-pipe-to-another-task-in-gulp)

### Use Package

### Compass

First, must install [compass](http://compass-style.org/install/)

[gulp-compass](https://www.npmjs.org/package/gulp-compass)

```javascript
var gulp = require('gulp');

var compass = require('gulp-compass');

gulp.task('default', function() {
  gulp.run('compass');

    gulp.watch([
        './sass/**',
        './img/**'
        ], function(event) {
        gulp.run('compass');
    });
});

gulp.task('compass', function() {
  gulp.src('./sass/*.scss')
    .pipe(compass({
        comments: false,
        css: 'css', // css folder
        sass: 'sass', // scss folder
        image: 'img' // image folder
    }));
});
```

commond

```sh
gulp
# or
gulp compass
```

### Jshint

[gulp-jshint](https://www.npmjs.org/package/gulp-jshint)

```javascript
var jshint = require('gulp-jshint');

gulp.task('lint', function() {
    return gulp.src('./*.js') // js file
    .pipe(jshint())
    .pipe(jshint.reporter('jshint-stylish'));
    // .pipe(jshint.reporter('default'))
});
```

commond

```sh
gulp lint
```

### Minify Html

[gulp-minify-html](https://www.npmjs.org/package/gulp-minify-html)

```javascript
var minifyHTML = require('gulp-minify-html');

gulp.task('minify-html', function() {
    var opts = {comments:true,spare:true};

    gulp.src('./*.html') // html file
    .pipe(minifyHTML(opts))
    .pipe(gulp.dest('./dist/')); // result minify html
});
```

commond

```sh
gulp minify-html
```

### Minify CSS

[gulp-minify-css](https://www.npmjs.org/package/gulp-minify-css)

```javascript
var minifyCSS = require('gulp-minify-css');

gulp.task('minify-css', function() {
    gulp.src('./css/*.css') // css files
    .pipe(minifyCSS({keepBreaks:true}))
    .pipe(gulp.dest('./dist/')); // result minify css
});
```

commond

```sh
gulp minify-css
```

### Minify JavaScript

[gulp-uglify](https://www.npmjs.org/package/gulp-uglify)

```javascript
var uglify = require('gulp-uglify');

gulp.task('uglify', function() {
    gulp.src('./*.js')
    .pipe(uglify())
    .pipe(gulp.dest('dist'));
});
```

commond

```sh
gulp compress
```
