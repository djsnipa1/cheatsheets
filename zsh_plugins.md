# zsh Plugins

## `z` 

### `z` Command Line Options

- `-c`    Only match subdirectories of the current directory
- `-e`    Echo the best match without going to it
- `-h`    Display help
- `-l`    List all matches without going to them
- `-r`    Match by rank (i.e. how much time you spend in directories)
- `-t`    Time -- match by how recently you have been to directories
- `-x`    Remove a directory (by default, the current directory) from the database
- `-xR`   Remove a directory (by default, the current directory) and its subdirectories from the database

### `z` Settings

Zsh-z has environment variables (they all begin with `ZSHZ_`) that change its behavior if you set them; you can also keep your old ones if you have been using `rupa/z` (they begin with `_Z_`).

* `ZSHZ_CMD` changes the command name (default: `z`)
* `ZSHZ_COMPLETION` can be `'frecent'` (default) or `'legacy'`, depending on whether you want your completion results sorted according to frecency or simply sorted alphabetically
* `ZSHZ_DATA` changes the database file (default: `~/.z`)
* `ZSHZ_ECHO` displays the new path name when changing directories (default: `0`)
* `ZSHZ_EXCLUDE_DIRS` is an array of directories to keep out of the database (default: empty)
* `ZSHZ_KEEP_DIRS` is an array of directories that should not be removed from the database, even if they are not currently available (useful when a drive is not always mounted) (default: empty)
* `ZSHZ_MAX_SCORE` is the maximum combined score the database entries can have before they begin to age and potentially drop out of the database (default: 9000)
* `ZSHZ_NO_RESOLVE_SYMLINKS` prevents symlink resolution (default: `0`)
* `ZSHZ_OWNER` allows usage when in `sudo -s` mode (default: empty)
* `ZSHZ_TILDE` displays the name of the `HOME` directory as a `~` (default: `0`)
* `ZSHZ_TRAILING_SLASH` makes it so that a search pattern ending in `/` can match the final element in a path; e.g., `z foo/` can match `/path/to/foo` (default: `0`)
* `ZSHZ_UNCOMMON` changes the logic used to calculate the directory jumped to; [see here](https://github.com/agkozak/zsh-z/blob/master/README.md#zshz_uncommon`) (default: `0`)

---
