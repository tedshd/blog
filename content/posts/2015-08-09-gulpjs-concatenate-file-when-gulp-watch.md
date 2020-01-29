---
layout: post
title: 'gulp.js - Concatenate File When Gulp Watch'
date: 2015-08-09
comments: true
categories: [javascript, gulp]
---
## gulp.js - Concatenate File When Gulp Watch

### package.json

```javascript
{
  "name": "gulp",
  "version": "3.8.7",
  "devDependencies": {
    "gulp": "^3.9.0",
    "gulp-concat": "^2.6.0",
    "gulp-watch": "^4.3.4"
  }
}
```

### gulpfile.js

```javascript
var gulp = require('gulp'),
    watch = require('gulp-watch'),
    concat = require('gulp-concat');

var js;
gulp.task('concat', function (cb) {
    var options = {};
    watch('dev/*.js', options, function (e) {
        // console.log('e:'+JSON.stringify(e));
        // console.log('\n');
        console.log(new Date() + ' -- ' + e.history[0].replace(e.base, ''));
        js = e.history[0].replace(e.base, '');
        gulp.src(['util/util.js', 'util/mod.js', 'dev/' + js])
        .pipe(concat(js, {newLine: '\n'}))
        .pipe(gulp.dest('dist/'));
    });
});
```

### What it mean?

watch something change in `dev/*.js`.

If js change, concatenate `util/util.js`, `util/mod.js` and current modify js.

New js name is current modify js.

Finally put new js in `dist/`.

### How to use

#### Install

```shell
npm install --save-dev gulp

npm install . --save-dev
```

#### Use

```shell
gulp concat
```

[Refer - gulp-watch](https://www.npmjs.com/package/gulp-watch)

[Refer - gulp-concat](https://www.npmjs.com/package/gulp-concat)
