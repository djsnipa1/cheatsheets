# Nix

## Garbage Collecting Error - Disk Full

If you try to 

# cd /nix/var/nix/db
# nix-shell -p sqlite

[nix-shell:/nix/var/nix/db]# sqlite3 db.sqlite ".backup 'db.bak.sqlite' "

[nix-shell:/nix/var/nix/db]# sqlite3 db.sqlite 
SQLite version 3.24.0 2018-06-04 19:24:41
Enter ".help" for usage hints.
sqlite> .output db.sql
sqlite> .dump
sqlite> 

[nix-shell:/nix/var/nix/db]# sqlite3 db.new.sqlite < db.sql

[nix-shell:/nix/var/nix/db]# mv db.new.sqlite db.sqlite
```

---
nix-env --delete-generations old
nix-collect-garbage
sudo nix-collect-garbage
We're down to 19.1 GiB
Let's do a full rebuild and make sure we're as compact as possible. Note that this removes old generations, make sure your system is stable first.
nix-channel --update
sudo nix-channel --update
sudo rm /nix/var/nix/gcroots/auto/*
nix-collect-garbage -d
sudo nix-collect-garbage -d
Down to 9.4 GiB
By hardlinking identical files we can save some additional space:
sudo nix-store --optimize
Now we're down to a nice trim 9.0 GiB - a savings of 15.1 GiB at the cost of losing some history.
Note that any shells you have will have to be rebuilt or refetched.
Pruning docker
I use docker for application development, this was done before but can save considerable space:
docker system prune
Note that this will delete a whole bunch of stuff, if you have any data not stored in volumes it will be lost.
Clearing your .cache folder
My .cache folder stands at 9.9 GiB
The highest amount is currently spotify. By editing ~/.config/spotify/prefs and adding:
storage.size=2048
then restarting spotify it will trim down its storage.
Next up is yarn.
yarn cache clean
saves me another 2.1 GiB
~/.local/share/Trash has considerable data in it, which after quick verification doesn't have anything I care about.
rm -rf ~/.local/share/Trash/files/*
rm -rf ~/.local/share/Trash/files/.*
After this I spent a bit poking around in ncdu and deleting old projects and forks that were not longer used.

---

## Get sha256 of URL or URL tarball

```bash
nix-prefetch-url https://github.com/NixOS/nixpkgs/archive/fksjflskjfsdlfkjslksjfsdlfkjdsj
```

```bash
nix-prefetch-url --unpack https://github.com/NixOS/nixpkgs/archive/fksjflskjfsdlfkjslksjflfk.tar.gz
```

## Get size of derivation or `nixpkgs`

```bash
nix-store -q —requisites `nix-build —no-out-link ‘<nixpkgs>’ -A vim` | sort -uf | xargs du -ch | tail -1
```

## Nix Package Manager

### Multiuser Installation

```bash
sh <(curl -L https://nixos.org/nix/install) —daemon
```
## Home Manager 

### Installation Non-NixOS

On non-nixos systems, install `nixFlakes` in your environment:

```bash
 nix-env -iA nixpkgs.nixFlakes
```

Edit either `~/.config/nix/nix.conf` or `/etc/nix/nix.conf` and add:

```
experimental-features = nix-command flakes
```

### Standalone installation

Make sure you have a working Nix installation. Specifically, make sure that your user is able to build and install Nix packages. For example, you should be able to successfully run a command like `nix-instantiate ‘<nixpkgs>’ -A hello` without having to switch to the root user. For a multi-user install of Nix this means that your user must be covered by the `allowed-users` Nix option. On NixOS you can control this option using the `nix.allowedUsers` system option.
Add the appropriate Home Manager channel. If you are following Nixpkgs master or an unstable channel you can run

```bash
$ nix-channel —add https://github.com/nix-community/home-manager/archive/master.tar.gz home-manager
$ nix-channel —update
```
and if you follow a Nixpkgs version 22.05 channel you can run

```bash
$ nix-channel —add https://github.com/nix-community/home-manager/archive/release-22.05.tar.gz home-manager
$ nix-channel —update
```
On non-NixOS, you may have to add

```bash
export NIX_PATH=$HOME/.nix-defexpr/channels:/nix/var/nix/profiles/per-user/root/channels${NIX_PATH:+:$NIX_PATH}
```
Run the Home Manager installation command and create the first Home Manager generation:

```bash
$ nix-shell ‘<home-manager>’ -A install
```
Once finished, Home Manager should be active and available in your user environment.

If you do not plan on having Home Manager manage your shell configuration then you must source the 
`$HOME/.nix-profile/etc/profile.d/hm-session-vars.sh`
file in your shell configuration. Alternatively source
`/etc/profiles/per-user/$USER/etc/profile.d/hm-session-vars.sh`
when managing home configuration together with system configuration.

This file can be sourced directly by POSIX.2-like shells such as Bash or Z shell. Fish users can use utilities such as foreign-env or babelfish.

For example, if you use Bash then add

`. “$HOME/.nix-profile/etc/profile.d/hm-session-vars.sh”` to your `~/.profile file.

If instead of using channels you want to run Home Manager from a Git checkout of the repository then you can use the programs.home-manager.path option to specify the absolute path to the repository.

Once installed you can see Chapter 2, Using Home Manager for a more detailed description of Home Manager and how to use it.


