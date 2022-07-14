# Nix

## Nix Package Manager

### Multiuser Installation

```bash
sh <(curl -L https://nixos.org/nix/install) --daemon
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
