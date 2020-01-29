---
layout: post
title: 'Sublime - change layout view in 2 columns'
date: 2014-02-27
comments: true
categories: [sublime-text]
---
## Sublime - change layout view in 2 columns

![output_T7Ok8b.gif](http://user-image.logdown.io/user/3170/blog/3202/post/181166/n0cayJWESiKZXwNBOvJa_output_T7Ok8b.gif)

Video

<iframe width="640" height="360" src="//www.youtube.com/embed/t9xq08x1tlw?rel=0" frameborder="0" allowfullscreen></iframe>

### Setting

`Preferences` -> `Key Bindings - User`

set key to use

```json
[
    {
        "keys": ["super+ctrl+left"],
        "command": "set_layout",
        "args":
        {
            "cols": [0.0, 0.95, 1.0],
            "rows": [0.0, 1.0],
            "cells": [[0, 0, 1, 1], [1, 0, 2, 1]]
        }
    },
    {
        "keys": ["super+ctrl+right"],
        "command": "set_layout",
        "args":
        {
            "cols": [0.0, 0.05, 1.0],
            "rows": [0.0, 1.0],
            "cells": [[0, 0, 1, 1], [1, 0, 2, 1]]
        }
    }
]
```

## **Update**

### Add focus

If add focus, it need 2 commands so need write a python plugin

1. `Tools` -> `New Plugin`

```python
# save as run_multiple.py
import sublime, sublime_plugin

# Takes an array of commands (same as those you'd provide to a key binding) with
# an optional context (defaults to view commands) & runs each command in order.
# Valid contexts are 'text', 'window', and 'app' for running a TextCommand,
# WindowCommands, or ApplicationCommand respectively.
class RunMultipleCommand(sublime_plugin.TextCommand):
  def exec_command(self, command):
    if not 'command' in command:
      raise Exception('No command name provided.')

    args = None
    if 'args' in command:
      args = command['args']

    # default context is the view since it's easiest to get the other contexts
    # from the view
    context = self.view
    if 'context' in command:
      context_name = command['context']
      if context_name == 'window':
        context = context.window()
      elif context_name == 'app':
        context = sublime
      elif context_name == 'text':
        pass
      else:
        raise Exception('Invalid command context "'+context_name+'".')

    # skip args if not needed
    if args is None:
      context.run_command(command['command'])
    else:
      context.run_command(command['command'], args)

  def run(self, edit, commands = None):
    if commands is None:
      return # not an error
    for command in commands:
      self.exec_command(command)
```

2. `Preferences` -> `Key Bindings - User`

```json
[
    {
        "keys": ["super+ctrl+left"],
        "command": "run_multiple",
        "args":
        {
            "commands": [
                {
                    "command": "set_layout",
                    "args":
                    {
                        "cols": [0.0, 0.95, 1.0],
                        "rows": [0.0, 1.0],
                        "cells": [[0, 0, 1, 1], [1, 0, 2, 1]]
                    },
                    "context": "window"
                },
                {
                    "command": "focus_group",
                    "args": { "group": 0 },
                    "context": "window"
                }
            ]
        }
    },
    {
        "keys": ["super+ctrl+right"],
        "command": "run_multiple",
        "args":
        {
            "commands": [
                {
                    "command": "set_layout",
                    "args":
                    {
                        "cols": [0.0, 0.05, 1.0],
                        "rows": [0.0, 1.0],
                        "cells": [[0, 0, 1, 1], [1, 0, 2, 1]]
                    },
                    "context": "window"
                },
                {
                    "command": "focus_group",
                    "args": { "group": 1 },
                    "context": "window"
                }
            ]
        }
    }
]
```

[Refer - how to create a custom layout in sublime text 2?](http://stackoverflow.com/questions/10913138/how-to-create-a-custom-layout-in-sublime-text-2)
[Refer - Custom layouts, Sublime text 2](http://stackoverflow.com/questions/13149800/custom-layouts-sublime-text-2)
[Refer - set_layout reference](http://www.sublimetext.com/forum/viewtopic.php?f=6&t=7284&start=0&hilit=set+layout)
Update
[Refer - Is it possible to chain key binding commands in sublime text 2?](http://stackoverflow.com/questions/9646552/is-it-possible-to-chain-key-binding-commands-in-sublime-text-2)
[Refer - nilium / key-bindings.json](https://gist.github.com/nilium/3327730)
