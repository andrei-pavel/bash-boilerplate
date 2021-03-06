# bash-boilerplate

![SVG](./cli.svg)

## Table of Contents

- [Libraries](#libraries)
    - [header](#header)
    - [spinner](#spinner)
    - [traps](#traps)
    - [utils](#utils)
    - [yaml-to-env](#yaml-to-env)
- [Example](#example)


## Libraries

All libraries are found inside `lib`.

Import any library with:
```bash
script_path="$(dirname "$(readlink -f "${0}")")"
. "${script_path}/lib/${library}"
```

They all have import guards to make sure no library is imported twice.

Make sure to import header first. It is a dependency to all other libraries.

### header

* ☑ `set -euo pipefail`
* ☑ `print-usage` function to print all `${ARGUMENTS}`
* ☑ default parameters `-c|--config $config_yaml` reads the given YAML file and
    converts all YAML variables to shell variables
* ☑ default parameters `-d|--debug` calls `set -x` for debug mode
* ☑ default parameters `-h|--help` calls `print-usage` automatically
* ☑ `add-to-usage` to add a custom message to the usage text
* ☑ `additional-arguments` function to print arguments other than the default
    ones above that were given to the script
* ☑ `additional-options` function to print arguments from the list above that
    were given to the script
* ☑ ANSII colors `${BLACK}`, `${RED}`, `${GREEN}`, `${YELLOW}`, `${BLUE}`,
    `${PURPLE}`, `${CYAN}`, `${WHITE}` are exported
* ☑ `argument` to define your argument and how it should be parsed
* ☑ `allow-extra-parameters` to allow more parameters than defined to be used
    directly in the script
* ☑ `parse-parameters` to parse the actual parameters
* ☐ support multiple-word extra parameters


### spinner

The best bash spinner out there

* ☑ `start-spinner ${text}` function to start a spinner with specified `${text}`
* ☑ `stop-spinner ${exit_code}` function to stop the spinner with success if
    `${exit_code}` is 0, with failure otherwise
* ☑ `disable-spinners` function to ignore commands that start and stop spinners
* ☑ `enable-spinners` function [default]
* ☑ `disable-verbose` function to print output on stopped spinner only if exit
    code was non-null [default]
* ☑ `enable-verbose` function to print output on stopped spinner all the time
* ☑ `configure-spinner-output [full-output|stdout-only|stderr-only|no-output]`
    function
* ☐ support nested spinners


### traps

* ☑ `traps [--force|--return-code-only] ${custom_trap}` function to set what
    runs after catching HUP, INT, QUIT, KILL, TERM, EXIT signals
    * usually captures return code, disables traps so that they don't run
        recursively, stops any spinners and then runs the `${custom_trap}`
    * `--force` makes it so that only `${custom_trap}` is run
    * `--return-code-only` skips over stopping the spinners which is needed in
        case you're not using spinners

### utils

* ☑ `confirm [${custom_question}]` function to ask the user a yes or no
    question
* ☑ `mandatory ${variable}` function to check if `${variable}` is set, `exit 2`
    otherwise
* ☑ `mandatory-command ${command}` function to check if `${command}` is
    available, `exit 3` otherwise


### yaml-to-env

* ☑ Simply importing it with
```bash
. "${script_path}/lib/yaml-to-env [${config_yaml}]"
```
will read `${config_yaml}` or `./config.yaml` if it is not provided and will
convert all YAML variables to shell variables just like
`-c|--config $config_yaml`, but programatically instead of user-requested.
* ☑ support for a second `-c config-yaml` in a child script


## Example

See the `hello-world` example which showcases how these features should be used.

```bash
Usage: hello-world {{options}} {{arguments}}
Options:
  [-c|--config $config_yaml]   Reads from a YAML configuration and converts all
                               key-value pairs with literal values to
                               environment variables.
  [-d|--debug]                 Enables debug mode, showing every executed
                               statement.
  [-h|--help]                  Prints usage (this text).
Arguments:
  [-a|--approval]              whether to ask user for approval
  -n $count                    print $count times
  [-y|--yaml $yaml]            specify path to the configuration file
  [$string]                    something other than "Hello, world!" to print
```
