---
layout: post
title: 'Vim config in Mac'
date: 2013-08-27
comments: true
categories: [Vim, mac]
---
## Some different in Mac

### PageDown, PageUp, Home, End

It is not useful in setting vimrc.

**Solution**
Terminal->Preference->KeyBoard
```config
Home:     \033[1~
End:      \033[4~
PageUp:   \033[5~
PageDown: \033[6~
```
