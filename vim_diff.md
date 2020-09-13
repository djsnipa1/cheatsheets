# VIM Diff

[vim - Merge changes using vimdiff - Stack Overflow](https://stackoverflow.com/questions/27832630/merge-changes-using-vimdiff)

You can use the following basic commands to merge:

* <kbd>d</kbd> <kbd>o</kbd> - Get changes from other window into the current window.
    
* <kbd>d</kbd> <kbd>p</kbd> - Put the changes from current window into the other window.
    
* <kbd>]</kbd> <kbd>c</kbd> - Jump to the next change.
    
* <kbd>[</kbd> <kbd>c</kbd> - Jump to the previous change.
    
* <kbd>z</kbd> <kbd>o</kbd> - Open folded lines.
    
* <kbd>z</kbd> <kbd>c</kbd> - Close folded lines.
    
* <kbd>z</kbd> <kbd>r</kbd> - Unfold both files completely.
    
* <kbd>z</kbd> <kbd>m</kbd> - Fold both files completely.
    
* <kbd>Ctrl</kbd> + <kbd>w</kbd> <kbd>w</kbd> - change window.
    
* `:only | wq` - quit other windows, write and quit.
    

## Quirks to watch for

* Both <kbd>d</kbd> <kbd>o</kbd> and <kbd>d</kbd> <kbd>p</kbd> work if you are on a block of change (or just one line under a single line of change) in Normal mode, but not in Visual mode.
    
* The undo command will only work in the buffer that was changed, so if you use <kbd>d</kbd> <kbd>p</kbd> and change your mind, you need to switch to the other buffer to undo.
    
* `:diffupdate` will re-scan the files for changes (Vim can get confused, and show bogus stuff).
    

## Visual mode and finer grained control

When selecting lines of text in Visual mode, you must use the normal commands:

* `:'<,'>diffget` and
* `:'<,'>diffput`.

For example:

1. Enter Visual mode and mark some text/lines.
2. Then type `:diffput` to push the selected lines to the other file or `:diffget` to get the selected lines from the other file.

To belabor the point: This means that if there is a block of changes consisting of multiple lines, then selecting a subset of lines and issueing `:diffput` will only apply those changes in the other buffer.

(`:diffget` and `:diffput` also accept ranges, see `:h copy-diffs` for more.)

## Compare two buffers inside Vim

If you load up two files in splits (`:vs` or `:sp`), you can do `:diffthis` on each window and achieve a diff of files that were already loaded in buffers.

`:diffoff` can be used to turn off the diff mode.

[This Vimcasts post and video](http://vimcasts.org/episodes/fugitive-vim-resolving-merge-conflicts-with-vimdiff/) show this in practice.

## How to apply all changes between buffers

0. Make sure that all participating buffers are in diff mode (see `:h start-vimdiff`)
    
1. a. Get changes from a buffer to the current one: `:%diffget <buffer-number>`
    
2. b. Put all changes from current buffer into another: `:%diffput <buffer-number>`
    

(`:%` is a range to select the entire file; see `:h :%`. `:ls` will show currently opened buffers.)

