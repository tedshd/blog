---
layout: post
title: 'Sublime Text - How to modify font size in sidebar'
date: 2016-09-01
comments: true
categories: [sublime]
---
## Sublime Text - How to modify font size in sidebar

In sublime text 3

If you want modify font size in sidebar

Follow step

1. Preferences -> Browse Packages
2. Open User directory
3. Create a file
4. File named your theme name
	* How to get it
	* Preferences -> Settings - User -> theme
	* Or default theme `Default.sublime-theme`
5. Add content
```JavaScript
[
	{
		"class": "sidebar_label",
		"font.size": 18
	},
]
```

### other

in Mac the path is

```
~/Library/Application Support/Sublime Text 3/Packages/User
```


[Reference - Sublime Text 3 how to change the font size of the file sidebar?](http://stackoverflow.com/questions/18288870/sublime-text-3-how-to-change-the-font-size-of-the-file-sidebar)
