# VIM

## vim-markdown 

## Mappings

The following work on normal and visual modes:

*   `gx`: open the link under the cursor in the same browser as the standard `gx` command. `<Plug>Markdown_OpenUrlUnderCursor`

    The standard `gx` is extended by allowing you to put your cursor anywhere inside a link.

    For example, all the following cursor positions will work:

    ```
    [Example](http://example.com)
    ^  ^    ^^   ^       ^
    1  2    34   5       6

    <http://example.com>
    ^  ^               ^
    1  2               3

    ```

    Known limitation: does not work for links that span multiple lines.

*   `ge`: open the link under the cursor in Vim for editing. Useful for relative markdown links. `<Plug>Markdown_EditUrlUnderCursor`

    The rules for the cursor position are the same as the `gx` command.

*   `]]`: go to next header. `<Plug>Markdown_MoveToNextHeader`

*   `[[`: go to previous header. Contrast with `]c`. `<Plug>Markdown_MoveToPreviousHeader`

*   `][`: go to next sibling header if any. `<Plug>Markdown_MoveToNextSiblingHeader`

*   `[]`: go to previous sibling header if any. `<Plug>Markdown_MoveToPreviousSiblingHeader`

*   `]c`: go to Current header. `<Plug>Markdown_MoveToCurHeader`

*   `]u`: go to parent header (Up). `<Plug>Markdown_MoveToParentHeader`

## A few helpful shortcuts related to executing things in the shell:

*   `:!` By itself, runs the last external command (from your shell history)
*   `:!!` Repeats the last commands
*   `:silent !{cmd}` Eliminates the need to hit enter after the command is done
*   `:r !{cmd}` Puts the output of $cmd into the current buffer.
*   `:r !{cmd} > filename` writes the output to a new file

## Using tabs in Vim

* Create a new tab with `:tabnew` 
* Open file in new tab `:tabnew filename`
* Open files in tabs from the command line

```shell
vim -p file1 file2 file3
```
* Search for open file in tabs with `:tabf filename`
* Search tabs with auto completion with `:tabn filename`
* Navigate tabs: Next = `:tabn` Previous = `:tabp` First tab = `:tabfirst` Last Tab = `:tablast`
* See list of open tabs with `:tabs`
* Move tab to a different position with `:tabm <ntab number>` _<tab number> is 0-whatever number tabs_ 
* Running commands in tabs:

> Let’s say you’re editing six or seven files in Vim and realize that you need to replace a variable name with a new one. Using the :tabdo command, you can run a search and replace through all of the tabs at once rather than changing each file individually. For instance, if you want to replace foo with bar, you’d run this:

```
:tabdo %s/foo/bar/g
```

That will run through each open tab and run the search and replace command (%s/foo/bar/g) in each one.

## Adding character before selected block of text

*   Press <kbd>Esc</kbd> to enter 'command mode'
*   Use <kbd>Ctrl</kbd> + <kbd>v</kbd> to enter visual block mode
*   Move Up/Down to select the columns of text in the lines you want to comment.
*   Then hit <kbd>Shift</kbd> + <kbd>i</kbd> and type the text you want to insert.
*   Then hit <kbd>Esc</kbd>, wait 1 second and the inserted text will appear on every line.

## Saving output to a file

Typically the output of the above commands will span several pages. You can use the following set of commands to redirect the output to the vim_maps.txt file:

```vim
:redir! > vim_maps.txt
:map
:map!
:redir END
```

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

## Copying whole document to clipboard

> On Windows & OS X there is no difference between `+` and `*`, since these systems only have a single clipboard, and both registers refer to the same thing (it doesn't matter which one you use).

You can use these registers as any register. For example, using the PRIMARY clipboard `*` with the `y` and `p` commands:

*   `"*yy`
*   `"*p`



