# replit 

## `replit.nix`

Trying to get the `unstable` neovim, I found [this](https://discourse.nixos.org/t/how-do-i-build-a-nix-shell-which-depends-on-some-unstable-packages/928/3)

```nix
let
  unstable = import (fetchTarball https://nixos.org/channels/nixos-unstable/nixexprs.tar.xz) { };
in
{ nixpkgs ? import <nixpkgs> {} }:
with nixpkgs; mkShell {
  buildInputs = [ hello unstable.neovim nixfmt ];
}
```
