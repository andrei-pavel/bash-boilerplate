# bash-boilerplate

## Table of Contents

- [Description](#description)
- [Usage](#usage)


## Description

The crux is in the files inside the lib directory which contains some header
scripts which aid in showing the usage of your script and in debugging it. `-h`
and `-d` arguments are built-in and you can easily add your own.


## Usage

Start with the hello-world script and place your logic below the ruler. Add
arguments inside the code block suggested by the `Parse arguments` code block
inside the `ARGUMENTS=` text block.

The provided example can be run in the following manner:
```
Usage: hello-world {{options}} {{arguments}}
Options:
  [-d|--debug]                 Enables debug mode, showing every executed statement.
  [-h|--help]                  Prints usage (this text).
Arguments:
  -n $count                    print $count times
  $string                      something other than "Hello, world!" to print
```

