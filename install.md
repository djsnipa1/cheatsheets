# Install

## Neovim from source

Install dependencies

```bash
sudo apt update
sudo apt-get install ninja-build \
     gettext libtool libtool-bin \
     autoconf automake cmake g++ \
     pkg-config unzip
```
Clone the `neovim` repo, build and install

```bash
git clone https://github.com/neovim/neovim.git
cd neovim
git checkout release-0.7
make CMAKE_BUILD_TYPE=Release
sudo make Install
```

### "Basic Stable IDE"
[LunarVim/nvim-basic-ide: This is my attempt at a basic stable starting point for a Neovim IDE.](https://github.com/LunarVim/nvim-basic-ide)

```bash
git clone https://github.com/LunarVim/nvim-basic-ide.git ~/.config/nvim
```


