---
layout: post
title: 'Sublime Text - initial setting'
date: 2013-09-01
comments: true
categories: [sublime-text]
---
## Initial Setting

[Sublime Text 手冊](http://docs.sublimetext.tw/)

**Preferences->Settings-Default**

```json
"default_encoding": "UTF-8"
"default_line_ending": "unix"
"tab_size": 4
"translate_tabs_to_spaces": true
"save_on_focus_lost": true
"highlight_line": true
"trim_trailing_white_space_on_save": true
"rulers": [80, 120]
"highlight_modified_tabs": true
```

choose

```json
"ensure_newline_at_eof_on_save": true
"use_simple_full_screen": true
```

if want change font size

**Preferences->Settings-User**

```json
{
    "default_encoding": "UTF-8",
    "default_line_ending": "unix",
    "tab_size": 4,
    "translate_tabs_to_spaces": true,
    "save_on_focus_lost": true,
    "highlight_line": true,
    "trim_trailing_white_space_on_save": true,
    "rulers": [80, 120],
    "highlight_modified_tabs": true,
    "font_size": 18.0,
    "ignored_packages":
    [
        "Vintage"
    ]
}
```
