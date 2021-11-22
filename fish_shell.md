# fish shell

## Showing a function or alias

```shell
# Replace function_name with your function or alias
type function_name
```

## adding `less` variable

Found the answer to this [here](https://stackoverflow.com/questions/27471823/zsh-global-alias-equivalent-in-fish-shell#comment43416010_27471823)

The only way I can see to code your specific example is :

```shell
function L; env $argv | less --chop-long-lines; end
``` 

and invoke with 

```shell
L echo "hello world"
```

-- obviously using a function as a command, not like a zsh global alias.

## Defining an Alias

1. Define alias in shell
```fish
alias rmi="rm -i"
```

2. Define alias in config file
```fish
alias rmi="rm -i"
```

3. This is equivalent to entering the following function:
```fish
function rmi
    rm -i $argv
end
```

4. Then, to save it across terminal sessions:
```fish
funcsave rmi
```

This last command creates the file `~/.config/fish/functions/rmi.fish`.


## Differences between bash and fish:

*   setting variables
    *   bash: `var=value`
    *   fish: `set var value`
*   function arguments
    *   bash: `"$@"`
    *   fish: `$argv`
*   function local variables
    *   bash: `local var`
    *   fish: `set -l var`
*   conditionals I
    *   bash: `[[ ... ]]` and `[ ... ]`
    *   fish: `test ...`
*   conditionals II
    *   bash: `if cond; then cmds; fi`
    *   fish: `if cond; cmds; end`
*   conditionals III
    *   bash: `cmd1 && cmd2`
    *   fish: `cmd1; and cmd2`
    *   fish (as of fish 3.0): `cmd1 && cmd2`
*   command substitution
    *   bash: `output=$(pipeline)`
    *   fish: `set output (pipeline)`
*   process substitution
    *   bash: `join <(sort file1) <(sort file2)`
    *   fish: `join (sort file1 | psub) (sort file2 | psub)`
