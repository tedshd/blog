---
layout: post
title: 'Sass compile two spaces'
date: 2013-11-20
comments: true
categories: [sass]
---
## Sass compile two spaces

Use Sass compile to css
css lndent is 2 spaces
if want 4 spaces
Must modify this sass source code
```sh
sass-3.2.10/lib/sass/tree/visitors/to_css.rb
```

```ruby
# before
tab_str = '  ' * (@tabs + node.tabs)
# after
tab_str = '    ' * (@tabs + node.tabs)
```

[Refer - Change indentation in Sass](http://stackoverflow.com/questions/13689264/change-indentation-in-sass)
