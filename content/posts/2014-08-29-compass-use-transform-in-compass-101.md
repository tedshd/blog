---
layout: post
title: 'Compass - Use transform in compass 1.0.1'
date: 2014-08-29
comments: true
categories: [css, Compass]
---
## Compass - Use transform in compass 1.0.1

On august 15, 2014
Compass release 1.0.1
Some code in scss change wording.
This article provide CSS3 transform wording in scss.

I use this Mixin

```scss
@import "compass/css3";
/*simple-transform($scale, $rotate, $trans-x, $trans-y, $skew-x, $skew-y, $origin-x, $origin-y)*/
@include simple-transform(1, 45deg, 5px, -15px, 0, 0, 0, 0);

/* Advance Usage */
/*@include create-transform($perspective, $scale-x, $scale-y, $scale-z, $rotate-x, $rotate-y, $rotate-z, $rotate3d, $trans-x, $trans-y, $trans-z, $skew-x, $skew-y, $origin-x, $origin-y, $origin-z, $only3d);*/
```

[Refer - Compass Transform | Compass Documentation](http://compass-style.org/reference/compass/css3/transform/#mixin-simple-transform)
