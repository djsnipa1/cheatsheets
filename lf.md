# `lf` file manager

|             key             | action              |
|:---------------------------:|---------------------|
|             `y`             | copy file           |
|             `d`             | cut file            |
|             `p`             | paste file          |
| `ctrl` + `u` & `ctrl` + `d` | half page up & down |
| `ctrl` + `b` & `ctrl` + `f` | full page up & down |
|                             |                     |

`copy` (default `y`) command copies the current file or selections, `cut` (default `d`) command cuts the current file or selections, `paste` (default `p`) command pastes the copied or cut files to the current directory, and `clear` (default `c`) command clears copied or cut files:

![yank-delete-put-clear](https://media.giphy.com/media/1j9eP2K2aAwbl3KLNT/giphy.gif)

`read` (default `:`) command reads a builtin or custom command:

![read](https://media.giphy.com/media/ir9xFlZM1z9cpDoGLo/giphy.gif)

`shell` (default `$`) command runs a command in the shell:

![shell](https://media.giphy.com/media/37nTncZlfehQl6Q3eB/giphy.gif)

`shell-pipe` (default `%`) command runs a command in the shell while piping the input from the ui and output to the ui:

![shell-pipe](https://media.giphy.com/media/9RZzRIN70lofjsuwxa/giphy.gif)

`shell-wait` (default `!`) command runs a command in the shell waits for a key press afterwards:

![shell-wait](https://media.giphy.com/media/3q1sMNb6XDR8EOdNDi/giphy.gif)

`shell-async` (default `&`) command runs a command in the background:

![shell-async](https://media.giphy.com/media/B1hN6oAFh7bw3Hg3J1/giphy.gif)

`search` (default `/`) command reads a pattern to search, `search-back` (default `?`) command searches in the opposite direction, `search-next` (default `n`) and `search-prev` (default `N`) find the next and previous file matching the pattern:

![search](https://media.giphy.com/media/pqxN1xOy2JSTDLLMQk/giphy.gif)

Some default keybindings are provided (prefixed with `z`) to toggle options or change their values:

![options](https://media.giphy.com/media/YVO0JEDh3sWXRaatf3/giphy.gif)

Some default keybindings are provided (prefixed with `s`) to change the values of `sortby` and `info` options:

![sorts](https://media.giphy.com/media/3KXbi0KRdu4kfDq9qq/giphy.gif)

Keybindings are provided to launch an editor (default `e`), a pager (default `i`), and a shell (default `w`):

![editor-pager-shell](https://media.giphy.com/media/58FNHPMoslq3Wi29Ls/giphy.gif)

# Configuration

You can download the example configuration file and customize according to your needs.
If you built from source you can simply copy this file from the repository:

    mkdir -p ~/.config/lf
    cp $GOPATH/src/github.com/gokcehan/lf/etc/lfrc.example ~/.config/lf/lfrc

Or if you installed a pre-built binary you can download this file from the repository:

    mkdir -p ~/.config/lf
    curl https://raw.githubusercontent.com/gokcehan/lf/master/etc/lfrc.example -o ~/.config/lf/lfrc

# Working Directory

`lf` starts in the current directory and changes the working directory accordingly when you move around.
On the other hand, when you quit `lf`, the launching shell remains in the starting directory.
This is a limitation of shells since it is not possible for a program to change the working directory of the parent process.
However, you can define a shell function for this purpose as a workaround if you want to stay on the last visited directory when you quit:

![lfcd](https://media.giphy.com/media/kE3fm0GzocYQkyqDVR/giphy.gif)

Example scripts are provided in the repository for common shells.
If you installed a pre-built binary you can download these example scripts from the repository:

    mkdir -p ~/.config/lf
    curl https://raw.githubusercontent.com/gokcehan/lf/master/etc/lfcd.sh -o ~/.config/lf/lfcd.sh

Then you need to source this file in your shell configuration file (e.g. `~/.bashrc`):

    LFCD="$GOPATH/src/github.com/gokcehan/lf/etc/lfcd.sh"  # source
    LFCD="/path/to/lfcd.sh"                                #  pre-built binary, make sure to use absolute path
    if [ -f "$LFCD" ]; then
        source "$LFCD"
    fi

You can also bind a key for this command if you like:

    bind '"\C-o":"lfcd\C-m"'

For other shells, see the comments in corresponding files for instructions.

# Multiple Terminals or Multiplexers

It is often useful to open a file manager in multiple paths at the same time to copy files between directories.
Instead of implementing tabs or panes, `lf` uses a server/client architecture for this purpose to fit your existing workflow.
A server process is automatically launched in the background when you run `lf` command for the first time.
This process saves the names of files to be copied or moved so that you can copy files in one client and paste them in another.
This feature requires no configuration and it can be used with either multiple terminals or a multiplexer such as `screen` or `tmux`:

![tmux](https://media.giphy.com/media/LVd3lzlMYSYDnVQbdO/giphy.gif)

# What Next?

You can read the [documentation](https://godoc.org/github.com/gokcehan/lf) for more in-depth information and the rest of the [wiki](https://github.com/gokcehan/lf/wiki) for extras.
