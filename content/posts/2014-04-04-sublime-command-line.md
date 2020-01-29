---
layout: post
title: 'Sublime - Command Line'
date: 2014-04-04
comments: true
categories: [mac sublime-text]
---
## Sublime - Command Line

in Mac OS X
make a symlink

```shell
ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" /bin/subl
// sublimetext 3
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /bin/subl
```

And Use it

```shell
subl --help
```

```shell
Usage: subl [arguments] [files]         edit the given files
   or: subl [arguments] [directories]   open the given directories
   or: subl [arguments] -               edit stdin

Arguments:
  --project <project>: Load the given project
  --command <command>: Run the given command
  -n or --new-window:  Open a new window
  -a or --add:         Add folders to the current window
  -w or --wait:        Wait for the files to be closed before returning
  -b or --background:  Don't activate the application
  -s or --stay:        Keep the application activated after closing the file
  -h or --help:        Show help (this message) and exit
  -v or --version:     Show version and exit

--wait is implied if reading from stdin. Use --stay to not switch back
to the terminal when a file is closed (only relevant if waiting for a file).

Filenames may be given a :line or :line:column suffix to open at a specific
location.
```

### Update

[Mac OS X 11中的/usr/bin 的“Operation not permitted”](https://www.jianshu.com/p/22b89f19afd6)

trun on power

`Command + R`

Go to recovery mode

Open terminal

```
csrutil disable
```

set bin shell

If want to disable

```
csrutil enable
```

[Refer - OS X Command Line](https://www.sublimetext.com/docs/2/osx_command_line.html)
