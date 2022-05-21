# Arch Linux

## `yay`

** update packages **
```shell
yay -Syyu
```

## `pacman`

**install package**

```shell
pacman -S <package name>
```

**update all installed packages**

```shell
pacman -Syu
```
**Clear pacman cache**

```shell
sudo pacman -Scc
```

**uninstall package**

```shell
sudo pacman -Rs
```

**remove unused packages**

```shell
sudo pacman -Rns (pacman -Qqtd)
```
---
## Using `debtap` to install a package

When there is no AUR package for something you are trying to install, you should try this method.

**install `debtap`**
```shell
yay -S debtap
```

**update the repos**
```shell
sudo debtap -u
```

**convert the `.deb` file**
```shell
sudo debtap filename.deb
```

**install the converted `.tar.zst` file**
```shell
sudo pacman -U filename.tar.zst
```
---

**clean the cache in `~/home` directory

```shell
sudo du -sh ~/.cache/
```

  my results:
  ![num3-clean-cache](images/num3-clean-cache.png)

  ![num3-clean-cache](https://github.com/djsnipa1/cheatsheets/blob/assets/images/num3-clean-cache.png)

  sha for image above:
  `abd33a8f83306b93bb69a767d0bf0ed4e2963843`

  ![num3-clean-cache](../assets/images/num3-clean-cache.png?raw=true)

  ![num3-clean-cache](https://github.com/djsnipa1/cheatsheets/assets/images/num3-clean-cache.png?raw=true)
---

