# bash-boilerplate

## Table of Contents

- [Description](#description)
- [Usage](#usage)


## Description

The crux is in the files inside the lib directory which contain some header
scripts which aid in showing the usage of your script and in debugging it.

`-h` and `-d` arguments are built into the header and you can easily add your
own inside the code block suggested by the `Parse arguments` comment and inside
the `ARGUMENTS=` text block.

See the `hello-world` example which showcases the different uses of these
arguments.


## Usage

```bash
Usage: hello-world {{options}} {{arguments}
Options:
  [-d|--debug]                 Enables debug mode, showing every executed statement.
  [-h|--help]                  Prints usage (this text).
Arguments:
  [-c]                         whether to ask user for confirmation
  -n $count                    print $count times
  [$string]                    something other than "Hello, world!" to print
```
