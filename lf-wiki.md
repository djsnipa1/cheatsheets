Most of the following tips assume that `ifs` option is set to `"\n"` and `shell` option is set to a posix compatible shell. You may need to adjust these to your setup accordingly.

# Enable Borders

If you want to have borders around the columns:
    
    set drawbox

# Dual pane single column mode

If you are used to file managers with single column directory views (e.g. midnight commander or far manager), there are a few settings you can use to get a similar feeling:

    set nopreview
    set ratios 1
    set info size:time

If you also want to have dual panes, you need to utilize a terminal multiplexer or your window manager. For `tmux` you may consider using a shell alias to automatically create dual panes:

    alias mc='tmux split -h lf; lf'

# Dynamically set number of columns

You can check the terminal width on startup and set number of columns accordingly:

    ${{
        w=$(tput cols)
        if [ $w -le 80 ]; then
            lf -remote "send $id set ratios 1:2"
        elif [ $w -le 160 ]; then
            lf -remote "send $id set ratios 1:2:3"
        else
            lf -remote "send $id set ratios 1:2:3:5"
        fi
    }}

You can also define this as a named command (e.g. `cmd recol &{{ .. }}`) and then call it once on startup (e.g. `recol`) so it will also be available as a command.

# Copy or move files on client instead of server

By default `lf` saves the names of files to be copied or moved on the server first so that you can for instance copy files in one client and paste them in another. If you don't need such use cases then you may consider remapping existing keys to work with selected files on the client instead of saving them on the server in advance:

    map y %cp -ri -- $fs .
    map d %mv -i -- $fs .
    map p

# Make backups when copying or moving

Unfortunately POSIX `cp` and `mv` commands do not define an option to backup existing files, but if you have the GNU implementation, you can define a custom `paste` command to use `--backup` option with these commands:

    cmd paste %{{
        set -- $(cat ~/.local/share/lf/files)
        mode="$1"
        shift
        case "$mode" in
            copy) cp -r --backup=numbered -- "$@" .;;
            move) mv --backup=numbered -- "$@" .;;
        esac
        rm ~/.local/share/lf/files
        lf -remote "send clear"
    }}

See `man cp` or `man mv` for more information.

# Copy and move files asynchronously

You can define an asynchronous paste command to do file copying and moving asynchronously:

    cmd paste &{{
        set -- $(cat ~/.local/share/lf/files)
        mode="$1"
        shift
        case "$mode" in
            copy) cp -rn -- "$@" .;;
            move) mv -n -- "$@" .;;
        esac
        rm ~/.local/share/lf/files
        lf -remote "send clear"
    }}

You can also define this command with a different name (e.g. `cmd paste-async &{{ .. }}`) and then bind it to a different key (e.g. `map P paste-async`) to use it selectively.

# Show progress for file copying

You can use an alternative file copying program that provides progress information such as `rsync` and feed this information to `lf` to display progress while coping files:

    cmd paste &{{
        set -- $(cat ~/.local/share/lf/files)
        mode="$1"
        shift
        case "$mode" in
            copy)
                rsync -av --ignore-existing --progress -- "$@" . |
                stdbuf -i0 -o0 -e0 tr '\r' '\n' |
                while IFS= read -r line; do
                    lf -remote "send $id echo $line"
                done
                ;;
            move) mv -n -- "$@" .;;
        esac
        rm ~/.local/share/lf/files
        lf -remote "send clear"
    }}

Information is shown at the bottom of the screen every second but it is overwritten for each action that also use this part of the screen.

# Use copy-on-write when possible

This snippet:

1. Tries to use CoW (reflinks) on btrfs, zfs and xfs
2. Falls back to lf's native paste **(keeps progress %)** if it can't
3. Handles matching names in destination with `.~1~` like lf
4. Forwards cp errors to status line, if any

Tested and works with `set shell bash` with `set shellopts '-eu'` (and GNU coreutils).

(Read before using)

```
cmd paste_try_cow &{{
    # # This was very helpful for debugging:
    # log_file="$HOME/lf-reflink-log-$(date +'%Y-%m-%d_%H-%M-%S')"
    # [ -f "$log_file" ] || touch "$log_file"
    # exec 1>> $log_file 2>&1
    # set -x

    # In theory, this may fail,
    # but I tested it on selection with 10k files - everything worked (bash)
    set -- $(cat ~/.local/share/lf/files)
    mode="$1"
    shift

    if [ $mode = 'copy' ]; then
        # Reflink if all items of selection and the destination are on the
        # same mount point and it is CoW fs.
        # (to make sure reflink never fails in first place, so we don't have to
        # clean up)

        src_targets="$(df --output=target -- "$@" | sed '1d' | sort -u)"

        if [ "$(df --output=target -- "$PWD" | tail -n 1)" = \
             "$(echo "$src_targets" | tail -n 1)" ] && \
             (( "$(echo "$src_targets" | wc -l)" == 1 )) && \
             [[ "$(df --output=fstype -- "$PWD" | tail -n 1)" =~ ^(btrfs|xfs|zfs)$ ]]; then

            echo 'selected copy and cp reflink paste'

            start=$(date '+%s')

            # Handle same names in dst
            # TODO parallelism, idk - but exit/return/break won't stop the loop from subshell...
            for i in "$@"; do
                name="${i##*/}"
                original="$name"

                count=0
                while [ -w "$PWD/$name" ]; do
                    count=$((count+1))
                    name="$original.~$count~"
                done

                set +e
                cp_out="$(cp -rn --reflink=always -- "$i" "$PWD/$name" 2>&1)"
                set -e

                if [ ! -z "$cp_out" ]; then
                    lf -remote "send $id echoerr $cp_out"
                    exit 0
                fi
            done

            finish=$(( $(date '+%s') - $start ))
            t=''
            if (( $finish > 2 )); then
                t="${finish}s"
            fi

            # Or just skip a file when names are the same.
            # (A LOT faster if you e.g. pasting selection of 10k files)
            # cp -rn --reflink=always -- "$@" .

            lf -remote "send clear"

            green=$'\u001b[32m'
            reset=$'\u001b[0m'
            lf -remote "send $id echo ${green}reflinked!${reset} $t"
        else
            echo 'selected copy and lf native paste'
            lf -remote "send $id paste"
        fi

    elif [ $mode = 'move' ]; then
        echo 'selected move and lf native paste'
        lf -remote "send $id paste"
    fi

    # # for debug
    # set +x

    lf -remote "send load"
}}

# name is different to avoid recursive calls
map p paste_try_cow
```

# Command/Mapping to create new directories

You can use the underlying `mkdir` command to create new directories.
It is possible to define a push mapping for such commands for easier typing as follows:

    map a push %mkdir<space>

You can also create a custom command for this purpose

    cmd mkdir %mkdir "$@"
    map a push :mkdir<space>

This command creates a directory for each argument passed by lf.
For example, `:mkdir foo 'bar baz'` creates two directories named `foo` and `bar baz`.

You can also join arguments with space characters to avoid the need to quote arguments as such:

    cmd mkdir %IFS=" "; mkdir -- "$*"
    map a push :mkdir<space>

This command creates a single directory with the given name.
For example, `:mkdir foo bar` creates a single directory named `foo bar`.

You can also consider passing `-p` option to `mkdir` command to be able to create nested directories (e.g. `mkdir -p foo/bar` to create a directory named `foo` and then a directory named `bar` inside `foo`).

If you want to select the new directory afterwards, you can call a remote `select` command as such:

```
cmd mkdir %{{
    IFS=" "
    mkdir -p -- "$*"
    lf -remote "send $id select \"$*\""
}}
```

# Use enviromental variable in command or mapping

You can't use environmental (shell) variables directly in mappings and internal commands.
You have to send variable to lf from shell scope using remote call. For example - when you want to map `g G` to `cd $GOPATH` you can use:

    map gG $lf -remote "send $id cd $GOPATH"

# Split words by default in `zsh`

`zsh` does not split words by default as described [here](http://zsh.sourceforge.net/FAQ/zshfaq03.html), which makes it difficult to work with `$fs` and `$fx` variables, but a compatibility option named `shwordsplit` (`-y` or `--sh-word-split`) is provided for this purpose.
You can set this option for all commands as such:

    set shell zsh
    set shellopts '-euy'
    set ifs "\n"
    set filesep "\n"  # default already

# Bulk rename multiple files

You can define a command to rename multiple files at the same time using your text editor to change the names.

    cmd bulk-rename ${{
        old="$(mktemp)"
        new="$(mktemp)"
        if [ -n "$fs" ]; then
            fs="$(basename $fs)"
        else
            fs="$(ls)"
        fi
        printf '%s\n' "$fs" >"$old"
        printf '%s\n' "$fs" >"$new"
        $EDITOR "$new"
        [ "$(wc -l < "$new")" -ne "$(wc -l < "$old")" ] && exit
        paste "$old" "$new" | while IFS= read -r names; do
            src="$(printf '%s' "$names" | cut -f1)"
            dst="$(printf '%s' "$names" | cut -f2)"
            if [ "$src" = "$dst" ] || [ -e "$dst" ]; then
                continue
            fi
            mv -- "$src" "$dst"
        done
        rm -- "$old" "$new"
        lf -remote "send $id unselect"
    }}

This command either works on selected files or non-hidden files in the current directory if you don't have any selection.

Another very compact possibility which renames the selected items only with ``vidir`` is:

```
map <f-2> $printf '%s\n' "$fx" | vidir -
```

Or, if you want more features, such as support for cyclic renames (A -> B, B -> A,...), for creating missing folders, `git mv`, and with safeguards against deleting / overwriting files, and without annoying numbers before filenames - consider using [dmulholl/vimv](https://github.com/dmulholl/vimv). 

(same name as another vimv, but this one is more feature rich and written in rust, don't forget to read its `--help`).

```
cmd bulkrename ${{
    vimv --git -- $(basename -a -- $fx)

    lf -remote "send $id load"
    lf -remote "send $id unselect"
}}

map R bulkrename
```


# Rename commands similar to those of ranger

Recent versions of Lf provide a builtin `rename` command. It is mapped by default to `r`. You can use the default mapping and command as is, or you can extend it so it'll feel a little bit more like in ranger.

```
# Unmap the default binding
map r
# Rename the file with a completely different name
map rc push :rename<space>
# Edit the current filename
map ra ${{
	# get 'basename' of the selection
	filename="${f##*/}"
	# quote it so we won't deal with quotes in the lf -remote command
	filename="$(printf '%q' "$filename")"
	filename="${filename// /<space>}"
	lf -remote "send $id push :rename<space>$filename"
}}
# Edit filename before the extension
map re ${{
	# get 'basename' of the selection
	filename="${f##*/}"
	# quote it so we won't deal with quotes in the lf -remote command
	filename="$(printf '%q' "$filename")"
	filename="${filename// /<space>}"
	lf -remote "send $id push :rename<space>$filename<a-b><c-b>"
}}
```

The following was tested with the following shell related Lf settings:

```
set shell zsh
set shellopts '-ey'
set ifs "\n"
```

See https://github.com/gokcehan/lf/issues/279 for more implementations.

# Create symlinks (soft / hard)

Here's a config snippet that adds a soft / hard symlinking command and mapping:

```
# y (select for copy) and P to paste soft-link
# d (select for cut) and P to paste hard-link
cmd link %{{
    set -- $(cat ~/.local/share/lf/files)
    mode="$1"
    shift
    if [ "$#" -lt 1 ]; then
        lf -remote "send $id echo no files to link"
        exit 0
    fi
    case "$mode" in
        # symbolically copy mode is indicating a soft link
        copy) ln -sr -t . -- "$@";;
        # while a move mode is indicating a hard link
        move) ln -t . -- "$@";;
    esac
    rm ~/.local/share/lf/files
    lf -remote "send clear"
}}
map P :link
```

`P` is used for both soft and hard linking. The "cut" mode of files donates a hard link is requested, while a "copy" mode donates a soft link is requested.

# Put lf into background
You might be missing the possibility to put the `lf` job into the background with the default `ctrl` and `z` keys.
```
map <c-z> $ kill -STOP $PPID
```

# Use `gio trash` if available

On systems that use GIO (Gnome Input/Output), such as Ubuntu, this will use the `gio
trash` command to move the currently selected items (files and dirs) to the trashcan. If
GIO is not available, it falls back to `mv`.

```
cmd trash ${{
    set -f
    if gio trash 2>/dev/null; then
        gio trash $fx
    else
        mkdir -p ~/.trash
        mv -- $fx ~/.trash
    fi
}}
```

Basic use of `mv` to implement a trashcan located in the user's home dir, as in the
fallback option here, has some noteable disadvantages:

  - If the items being moved to trash are not on the same filesystem as the user's home
  dir, they are moved between filesystems with potentially lengthy copy+delete operations.

  - Items in trash take up storage in the filesystem holding the user's home dir instead
  of the filesystem they were initially in.

  - Since items with the same name will overwrite each other if they're moved to the same
  dir, items with common names easily become overwritten and unrecoverable.

  - The OS does not know that files moved to trash are probably less important to the user
  than the user's other files, so will not suggest them for deleting when running low on
  disk space and may included them in automated backups, etc.

  - The OS does not provide any functionality that helps finding and restoring
  accidentally deleted files to their original locations.

`gio trash`, however, implements a trashcan without any of the disadvantages listed
above. Instead of moving items across filesystems, it creates trash dirs as required on
the filesystems where the items alread are. Items are stored with metadata containing
original names and locations, preventing overwrites. The OS suggests deleting items from
the trash when running low on space. Functionality for finding files that were moved to
trash and restoring them to their original locations is available.

# New folder with selected item(s)

A function similar to macOS Finder.app

If you use `zsh`, make sure you `set shellopts '-euy'` as described above for proper `$fx` split.

```
map <a-n> newfold

cmd newfold ${{
    set -f
    read newd
    printf "Directory name: "
    mkdir -- "$newd"
    mv -- $fx "$newd"
}}
```

# Add to cut/copied files

Like rangers `da` and `dr`. Implementing this for copying files is mostly the same, simply rename `move` to `copy` where applicable.

NOTE this can also be used to switch a file selection from move to copy or vice versa.

WARN `$'\n'` is not POSIX compliant.

```
cmd cut-add %{{
    files=$(lf -remote load | tail -n +2)
    newline=$'\n'

    # change to $fx to add current file when no toggled
    # files exist.
    if [ -n "$files" ]; then
        new_files=$(echo "$files${newline}$fs" | sort | uniq)
    else
        new_files=$fs
    fi
    # remove empty lines from the file list, because they keep messing
    # up the selection.
    new_files=$(echo "$new_files" | sed --quiet -e '/^$/d' -e 'p')

    lf -remote "save${newline}move${newline}${new_files}${newline}"
    lf -remote "send $id unselect${newline}send $id sync"
}}

cmd cut-remove %{{
    files=$(lf -remote load)
    operation=$(echo "$files" | head -n1)

    if [ "$operation" != "move" ]; then
        lf -remote "send $id echoerr no files in cut list."
        exit 1
    fi

    files=$(echo "$files" | tail -n +2)
    newline=$'\n'

    # change to $fx to remove current file when no toggled
    # files exist.
    if [ -n "$files" ]; then
        # here we want all files in $files that aren't in $fs, making sure
        # that none of the entries in $fs are included, even when they aren't
        # in $files. To do this we concatenate $files and $fs (twice), printing
        # only the uniqe lines.
        new_files=$(echo "$files$newline$fs$newline$fs" | sort | uniq -u)
    else
        new_files=$files
    fi
    new_files=$(echo "$new_files" | sed --quiet -e '/^$/d' -e 'p')

    lf -remote "save${newline}move${newline}${new_files}${newline}"
    lf -remote "send $id unselect${newline}send $id sync"
}}
```

# Yank paths into your clipboard

the following commands each use xclip to copy files onto your clipboard. This depends on xclip so it probably won't work on windows. I suggest anyone who wants to use it cross platform create a script to automate platform dependent clipboard tools and then replace `xclip` below with that script. These commands strip the trailing line break.

```
cmd yank-dirname $dirname -- "$f" | head -c-1 | xclip -i -selection clipboard
cmd yank-path $printf '%s' "$fx" | xclip -i -selection clipboard
cmd yank-basename $basename -a -- $fx | head -c-1 | xclip -i -selection clipboard

cmd yank-basename-without-extension ${{
    echo "$fx" |
      xargs -r -d '\n' basename -a |
      awk -e '{
        for (i=length($0); i > 0; i--) {
          if (substr($0, i, 1) == ".") {
            if (i == 1) print $0
            else print substr($0, 0, i-1)

            break
          }
        }

        if (i == 0)
          print $0
      }' |
      if [ -n "$fs" ]; then cat; else tr -d '\n'; fi |
      xclip -i -selection clipboard
}}
```

Here's an alternative implementation of `yank-basename-without-extension`

```
cmd yank-basename-without-extension &basename -a -- $fx | rev | cut -d. -f2- | rev | head -c-1 | xclip -i -selection clipboard
```

Here's another implementation which treats any character after the first "." as part of the extension.

```
cmd yank-basename-without-extension &basename -a -- $fx | cut -d. -f1 | head -c-1 | xclip -i -selection clipboard
```

# Ranger's open_with

```
cmd open-with %"$@" "$fx"
map ` push :open-with<space>
```

# Run a command with spaces escaped

```
cmd run-escaped %{{
  IFS=" "
  cmd="$1"
  shift
  "$cmd" "$*"
}}
map \\ push :run-escaped<space>
```

# Share any file 256MiB limit

returned url wil be appended to clipboard (linux) edit to pbcopy for osx

    cmd share $curl -F"file=@$fx" https://0x0.st | xclip -selection c

# Toggle preview with the `i` key (with the `less` pager)
In `lf` the `i` key is the default for previewing files. It is convenient to let `i` also quit the `less` pager. Hence you uses the same key to open preview and to close it, and here is how to do:
```
$ echo "i quit" > ~/.config/lf/less
$ lesskey -o ~/.config/lf/less.lesskey ~/.config/lf/less
```
In the `lf` config activate the preview and set the preview script for less to use this cusom key binding.
```
set preview
set previewer "less -k ~/.config/less.lesskey"
```

# select all files or directories in the current directory

```
cmd select-files ${{
    { echo "$fs"; find -L "$(pwd)" -mindepth 1 -maxdepth 1 -type f; } |
        if [ "$lf_hidden" = "false" ]; then
          # remove any hidden files so you only select files you can see.
          grep -v '/\.[^/]\+$'
        else
          cat
        fi |
        sed '/^$/d' | sort | uniq -u |
        xargs -d '\n' -r -I{} lf -remote "send $id toggle {}"
}}

cmd select-dirs ${{
    { echo "$fs"; find -L "$(pwd)" -mindepth 1 -maxdepth 1 -type d; } |
        if [ "$lf_hidden" = "false" ]; then
          grep -v '/\.[^/]\+$'
        else
          cat
        fi |
        sed '/^$/d' | sort | uniq -u |
        xargs -d '\n' -r -I{} lf -remote "send $id toggle {}"
}}
```

# Show current directory in window title

This is useful if you e.g. want to use [rofi](https://github.com/davatorium/rofi) to search for specific instance of lf.

In shell you could change the title of your terminal to current directory with

```sh
printf "\033]0; $PWD\007"
```

However, it's not a standard, so it doesn't work in some terminals. I found it working in [alacritty](https://github.com/alacritty/alacritty), [st](http://st.suckless.org/), [kitty](https://github.com/kovidgoyal/kitty) and [rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html), but not in e.g. KDE's [konsole](https://konsole.kde.org/) (haven't tested others).

We could utilize this escape sequence in lf via special `on-cd` command, which runs when directory is changed.

```sh
cmd on-cd &{{
    # '&' commands run silently in background (which is what we want here),
    # but are not connected to stdout.
    # To make sure our escape sequence still reaches stdout we pipe it to /dev/tty
    printf "\033]0; $PWD\007" > /dev/tty
}}

# also run at startup
on-cd
```

If you want to show `~` instead of `/home/username`, change printf line to

```sh
printf "\033]0; $(pwd | sed "s|$HOME|~|")\007" > /dev/tty
```

It might also be useful to show a program name.

```sh
printf "\033]0; $(pwd | sed "s|$HOME|~|") - lf\007" > /dev/tty
```

<details>
  <summary>demo of the first version</summary>

  ![demo gif](https://user-images.githubusercontent.com/14999778/92522474-73488400-f227-11ea-9300-5daf537d6291.gif)

  (it actually changes instantly, i just pull updates only once per second)
</details>

# Warn about nested instances

Add the following to your `lfrc` to show a warning on startup if `lf` is running as a nested instance:

    %[ $LF_LEVEL -eq 1 ] || echo "Warning: You're in a nested lf instance!"

# Show nesting level in [powerlevel10k](https://github.com/romkatv/powerlevel10k) zsh prompt

To show the current nesting level (`$LF_LEVEL`) in your prompt when using p10k, add the following to your `p10k.zsh` config file:

1. Add the following function anywhere in the config file. Replace "📂" with whichever icon you want to use and is supported by your terminal/font.

```
  function prompt_lf() {
    p10k segment -f 208 -i '📂' -t "$LF_LEVEL" -c "$LF_LEVEL"
  }
```

2. Add `lf` to your prompt ( `POWERLEVEL9K_LEFT_PROMPT_ELEMENTS` or `POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS` at the top of the file)

This prompt segment will only be shown when the shell is "nested" in an lf instance. 

# Searchable bookmarks

First, set an environment variable called `LF_BOOKMARK_PATH` to an empty folder which will contain your bookmarks, then add the following to your `lfrc`.

```sh
cmd bookmark_jump ${{
    res="$(cat $LF_BOOKMARK_PATH/$(ls $LF_BOOKMARK_PATH | fzf))"
    lf -remote "send $id cd \"$res\""
}}

cmd bookmark_create ${{
    read ans
    echo $PWD > $LF_BOOKMARK_PATH/$ans
}}