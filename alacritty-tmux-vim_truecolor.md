This should make True Color (24-bit) and italics work in your [tmux](https://github.com/tmux/tmux/wiki) session and [vim](https://github.com/vim/vim) when using [Alacritty](https://github.com/alacritty/alacritty) (and should be compatible with any other terminal emulator, including [Kitty](https://github.com/kovidgoyal/kitty)).

Tested successfully in [bash](https://www.gnu.org/software/bash/) and [zsh](https://www.zsh.org/) with latest packages from [Arch Linux](https://archlinux.org/) (with exception of [neovim](https://github.com/neovim/neovim) built from source):
* ~~2019-07-07~~
* 2021-08-07

## Notes

1. _**Don't**_ use `&t_8f`, `&t_8b` and `t_Co` in your vim config
2. _**Don't**_ set `$TERM` in your zshrc, bashrc, etc. Configure this in your terminal (alacritty).
3. [Alacritty has no undercurl support](https://github.com/alacritty/alacritty/issues/1628), even though [tmux has](https://github.com/tmux/tmux/issues/1492)

## Testing colors

Running this script should look the same in tmux as without.

```shell
curl -s https://gist.githubusercontent.com/lifepillar/09a44b8cf0f9397465614e622979107f/raw/24-bit-color.sh >24-bit-color.sh
bash 24-bit-color.sh
```

![colors](https://user-images.githubusercontent.com/161548/128653955-45b190c8-a5b8-4c37-9a69-67551cd955ac.png)

## Configuration files

### Alacritty

In `~/.config/alacritty/alacritty.yml`:

```yaml
env:
  TERM: xterm-256color
```

### tmux

In `~/.tmux.conf` (or `~/.config/tmux/tmux.conf`):

```tmux
set -g default-terminal "tmux-256color"
set -ag terminal-overrides ",xterm-256color:RGB"
```

### vim (neovim)

In `~/.vimrc` or `~/.config/nvim/init.vim`:

```vim
set termguicolors
colorscheme yourfavcolorscheme
```

or `~/.config/nvim/init.lua`:

```lua
vim.o.termguicolors = true
vim.cmd'colorscheme yourfavcolorscheme'
```