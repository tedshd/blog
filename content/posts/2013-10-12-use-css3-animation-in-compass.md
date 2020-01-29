---
layout: post
title: 'Use CSS3 animation in Compass'
date: 2013-10-12
comments: true
categories: [css, sass, Compass]
---
## Use CSS3 Animation In Compass

Compass default dosen't have mixin in CSS3 animation
We can use this method in **scss**
```scss
/* define */
$animation-support: webkit, moz, o, ms, not khtml;

/* use */
.animation {
    @include experimental('animation-name', move, $animation-support);
    @include experimental('animation-duration', 5s, $animation-support);
    @include experimental('animation-iteration-count', 1, $animation-support);
}
```

and add ```keyframes```
```scss
/* define */
$animation-support: webkit, moz, o, ms, not khtml;
@mixin keyframes($name) {
    @-webkit-keyframes #{$name} {
        @content;
    }
    @-moz-keyframes #{$name} {
        @content;
    }
    @-ms-keyframes #{$name} {
        @content;
    }
    @keyframes #{$name} {
        @content;
    }
}

/* use */
.animation {
    @include experimental('animation-name', move, $animation-support);
    @include experimental('animation-duration', 5s, $animation-support);
    @include experimental('animation-iteration-count', 1, $animation-support);
}

@include keyframes(move) {
    0% {
        top: 780px;
        opacity: 0;
    }
    100% {
        top: 450px;
    }
}
```

[Refer - keyframes-sass-output.css](https://gist.github.com/ericam/1607696)
[Refer - Getting Compass to add vendor prefixes to animation selectors](http://stackoverflow.com/questions/17618082/getting-compass-to-add-vendor-prefixes-to-animation-selectors)
