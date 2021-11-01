# fish shell

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
