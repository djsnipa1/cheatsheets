# VIM

## A vim “delete blank lines” command

To delete *blank lines* in vim (empty lines), use this vim command in “last line mode”:

```
:g/^$/d
```
Here’s a brief explanation of how this vim “delete blank lines” command works:

> * The `:` character says, “put vim in last\-line mode.”

> * The `g` character says, “perform the following operation globally in this file.” (Operate on all lines in this file.)

> * The forward slash characters enclose the pattern I’m trying to match. In this case I want to match blank lines, so I use the regular expression `^$`. Here the `^` means “beginning of line,” and `$` means “end of line,” so with no characters in between them, this vim regex means “blank line.” (If I had typed `^abc$`, that would mean, “find a line with only the sequence of characters ‘abc’”.)

> * The `d` at the end of the command says, “When you find this pattern, delete the line.”

## Delete columns of characters

1.  Place cursor on first or last character you want to delete

2.  Press <kbd>Ctrl</kbd> + <kbd>v</kbd> to enter Visual Block mode

3.  Use arrow keys to select the characters you want to delete (or the other "*first few characters*")

4.  Press <kbd>x</kbd> to delete them all at once

## Writing to file with sudo

```
:w !sudo tee %
```

Add this to `.config/nvim/init.vim`:

```
" Allow saving of files as sudo when I forgot to start vim using sudo.
cmap w!! w !sudo tee > /dev/null %
```


