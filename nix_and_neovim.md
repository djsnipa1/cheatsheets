---
title: Neovim & Nix
created: "2022-07-14 17:49"
modification date: "2022-07-14 17:49"
tags: tutorial neovim nix article
link: "https://justin.restivo.me/posts/2021-10-24-neovim-nix.html"
---
# [Justin Restivo - A Portable Text Editor: Nix <3 Neovim](https://justin.restivo.me/posts/2021-10-24-neovim-nix.html)
This post was borne out of my frustrations of repeatedly switching between developing on different servers with various versions of linux installed under the constraints of not having root permissions. Setting up neovim with all the tools I’m used to was quite tedious. My workflow was as follows:

* Clone Neovim nightly (it consistently has really cool features!), install its deps, build it, and stick the result in `$HOME/usr/bin` and add `$HOME/usr/bin` to my `$PATH`.
* Intall system dependencies such as ripgrep or fd.
* Install Vim Plug, wget a gist with my vimrc config in it, and finally, `:PlugInstall`.
* Install all the language servers I needed. This was the hard part, as that process differed for each language server. Some I grabbed off a github release, others I built manually from source as to get the most up-to-date version.

This might take me 1-2 hours overall, and is both frustrating and tedious to set up and maintain on a large scale. Each computer is slightly different. My “solution” using `nix` turns this into 20 seconds on any linux machine with 3 commands. Fast and easy:

```
git clone https://github.com/DieracDelta/vimconf_talk.gitcd vimconf_talk &&bash setup.shsource$HOME/.bashrc &&nix run .
```

Please note that the work I’m describing here is not original. I’m (per usual) trying to make something that is reasonably complex understandable to a wider audience. Special thanks to:

* [Zach Coyle’s](https://github.com/zachcoyle)[Neovitality Nix distribution](https://github.com/vi-tality/neovitality) was my inspiration for this post. I present a *very* simple version of what’s possible with Nix. Neovitality reaches for the stars and shows just how much is possible.
* [Shadow’s](https://github.com/shadowninja55) neovim configuration was a great starting point to figure out “how” to configure neovim with Lua.
* [Gytis](https://github.com/gytis-ivaskevicius) for all the effort he poured into making the vim “nix” experience much better. I’m really enthused to see where his [vim2nix](https://github.com/gytis-ivaskevicius/nix2vim) project goes.

This is meant to have a low barrier for entry. I intend the readers to be strangers to the Nix ecosystem (Nix may not even be installed!) but are familiar with configuring Neovim with lua, neovim plugins, and linux.

One can either do an install of the nix onto their distribution of linux or use DavHau’s `nix-portable` project. I opt for the latter approach, since it’s easier to set up and less commitment overall (no nix users need to be made and no read only file system is mounted). I wrote some wrapper scripts to ease the setup workflow that I’ll explain here:

```
#!/usr/bin/env bashNIX_PORTABLE_LOC="$PWD"wget https://github.com/DavHau/nix-portable/releases/download/v008/nix-portablechmod +x nix-portableNP_LOCATION=$NIX_PORTABLE_LOCNP_RUNTIME='bwrap'$PWD/nix-portable nixprintf"\nsubstituters = https://cache.nixos.org https://jrestivo.cachix.org \ntrusted-public-keys = cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY= jrestivo.cachix.org-1:+jSOsXAAOEjs+DLkybZGQEEIbPG7gsKW1hPwseu03OE=\n">>$NIX_PORTABLE_LOC/.nix-portable/conf/nix.confprintf"\nalias nix=\"NP_LOCATION=$NIX_PORTABLE_LOC NP_RUNTIME='bwrap' $PWD/nix-portable nix\"\n">>$HOME/.bashrc
```

Nix portable is an awesome project that spins up an unprivileged container with `nix` and `flakes` installed. We first snag the `nix-portable` executable (bash script) on line 2, then run it on line 5. We tell `nix-portable` to use `$PWD/.nix-portable` as its container root directory by setting `NP_LOCATION`, and to use bubblewrap by setting `NP_RUNTIME` to bubblewrap.

Line 6 sets up the binary cache. The idea is to have Github CI (we’ll get to this later) build neovim from source with our configuration and all our language servers/plugins and push it to a binary cache (using Cachix). We’ll then pull down this “built” artifact from the binary cache on the server we wish to run on.

We’ll be generating our vim configuration using `nix`. As a result, there’s an `edit.sh` script that will listen for writes to the `flake.nix` file and regenerate our configuration based on its output. We’ll set `autoload` in neovim to listen for the change to the generated lua config. The edit script:

```
#!/usr/bin/env bash# remember to set autoread in vim to autorefresh the file in vimNIX_PORTABLE_LOC="$PWD"find ./*.nix |entr-r bash -c"NP_LOCATION=$NIX_PORTABLE_LOC NP_RUNTIME='bwrap' $PWD/nix-portable nix build .#neovimConfig -o init.nvim_store && cp -f $NIX_PORTABLE_LOC/.nix-portable/store/\$(basename \$(readlink $PWD/init.nvim_store)) $PWD/init.nvim"
```

`entr` is used to listen for a change to nix files. Note that `entr` may need to be installed (`apt-get install -y entr` on Debian based distros). Upon change, we use `nix-portable` to build the config (`.#my_config`) and stick it in `$PWD/init.nvim_store`. However, this is a broken symlink to the nix store (nix-portable specific problem), and needs to be replaced. Some bash wizardry is used to recreate the path to the nix store from its location in `$PWD/.nix-portable/store`.

The repo I’ll be explaining is located [here](https://github.com/DieracDelta/vimconf_talk/blob/0_initial_flake/flake.nix). Check out the `0_initial_flake`, as this will be our starting point. The idea is to (hopefully) follow along as I explain how to configure neovim in a portable manner. The hope is that by the end of this, the reader will be able to fork my repo as a template and use it to configure their own portable vim “distro”.

The `flake.nix` is written in the Nix language and defines our vim configuration. Think a JSON like language with ML-style (MetaLanguage not machine learning) syntax and lambda functions. Let’s analyze the code. The top level looks like:

```
{
  inputs = { ... };
  outputs = inputs@{...}: {
  }
}
```

This can be thought of as a “pure” function in a similar sense to other functional languages like Haskell. We input a set of pinned source code, and then the `nix` compiler builds some set of output build artifacts. The *key* subtlety is that these outputs are *always* the same for the same set of inputs (this is a lie, but a useful one for abstraction purposes). For the inputs, I’ve added neovim nightly (which has its own nix flake!), some vim plugins that I want to run on master, my home-brewn “nix to lua” translator/helper functions, and `rnix-lsp`–a language server for Nix written in Rust.

Now, let’s consider the outputs. The outputs are a function of the inputs: `inputs` refers to the entire attribute set (analagous to JSON), and the `{neovim, ...}` will destructure that attribute set one level. For example `neovim` binds to `inputs.neovim`.

Now I declare some variables:

```
neovimConfig = ...;
customNeovim = DSL.neovimBuilderWithDeps.legacyWrapper neovim.defaultPackage.x86_64-linux {
  extraRuntimeDeps = [];
  withNodeJs = true;
  configure.customRC = my_config;
  configure.packages.myVimPackage.start = with pkgs.vimPlugins; [ ];
};
```

Conceptually:

* `neovimConfig` is where any plaintext config that would normally end up in a `init.lua` lives.
* `customNeovim` is the final product. I use my `DSL`’s legacyWrapper. Normally this would come from `nixpkgs` (monorepo for all nix packages), but then it is difficult to pass in runtime dependencies. I’ve added the `extraRuntimeDeps` attribute to handle that in its own function exported from my DSL flake. `withNodeJs` builds the nodejs runtime into neovim, and `customRC` inserts `my_config` as our lua config file (albeit wrapped in a `init.nvim`). `configure.packages.myVimPackage.start` specifies a list of vim packages to make available when Neovim starts. `neovim.defaultPackage.x86_64-linux` builds our neovim off of the nightly `neovim` input.

The syntax might be intimidating at this point, but don’t sweat too much. The idea isn’t to question this template, as it should “just workTM”. This initial layer of abstraction will allow us to create a powerful and portable vim build.

We may use these variables we’ve defined to create outputs:

```
{
        # The packages: our custom neovim and the config text file
        packages = { inherit (pkgs) customNeovim neovimConfig; };

        # The package built by `nix build .`
        defaultPackage = pkgs.customNeovim;

        # The app run by `nix run .`
        defaultApp = {
          type = "app";
          program = "${pkgs.customNeovim}/bin/nvim";
        };
};

```

Sidenote: experienced Nixers would expect defaultApp not to be required (`nix run` should automatically work and does quite well on normal Nix installs. This is a nix-portable quirk).

We can inspect these outputs.

```
$ nix flake show
git+file:///home/jrestivo/Projects/vimtalk
├───defaultApp
│   └───x86_64-linux: app
├───defaultPackage
│   └───x86_64-linux: package 'neovim-master'
└───my_config: unknown
```

There are a few things we may do with this. First:

```
bash edit.sh
```

This will build our lua config on change to our flake. We can then open `init.nvim` and have a look at the generated lua inside. To do this manually, we may run `nix build .#my_config`.

Next, the `defaultPackage.x86_64-linux` attribute will build our “customized” neovim and store the resulting build artifacts in a `result` directory:

`nix build .`

Finally, the `app` attribute will let us run `neovim` without having the repo cloned. We may either

```
nix run github:DieracDelta/vimconf_talk# ORnix run .
```

This CLI is very convenient to use from a user perspective. What I typically do on servers is (1) install nix-portable (run `./setup.sh`) and then (2) alias vim to `nix run github:DieracDelta/vimconf_talk`. Then I get all the NeoVim loveliness but setup is trivialized. *This* is the power of Nix.

Now that we understand the set up, all that remains is to fill out the rest of the config to make it useful.

Check out branch `1_dsl` to see the `DSL` in action. Keybinds are just lua calls. They have a natural representation in Nix as a JSON-like attribute set. For this, we use Gytis’ [nix2vim](https://github.com/gytis-ivaskevicius/nix2vim). For example:

```
  nnoremap.j = "gj";
```

This translates to: `vim.api.nvim_set_keymap('n','j','gj',{ noremap = true})`.

Similarly `vim.o` and `vim.g` settings may be thought of the same way:

```
vim.g = {
  mapleader = " ";
  nofoldenable = true;
  noshowmode = true;
  completeopt = "menu,menuone,noselect";
};
vim.o = {
  termguicolors = true;
  ...
}
```

Sometimes we may also need to call lua functions. There isn’t an easy way to do this (yet) from nix. So, instead we call directly from the raw rc attribute.

```
configure.customRC = ''
  colorscheme dracula
  luafile ${neovimConfig}
'';

```

which enables syntax highlighting in Neovim then loads the config file.

Check out branch `2_plugins`. Most plugins have been already packaged and live in `nixpkgs`. To see, we can run:

```
nix search nixpkgs $PLUGINNAME
```

Often times, the source is out of date. To tell, we can look at the revision:

```
nix edit nixpkgs#$PLUGINNAME
```

Now, I’ve gone through and done this for most of the plugins I use on a day-to-day basis. For the out of date ones, I add nix flake inputs and call `overrideAttrs`. `overrideAttrs` is a function that takes a function as an input of the form `(oldattrs: {...})`. This function takes in one argument, `oldattrs`, and returns an attribute set which is then merged with the old attribute set. It overwrites any attributes we specify. In this case, we just wish to override the source code (which we have done in multiple places). We write a wrapper around this called `withSrc`.

```
      withSrc = pkg: src: pkg.overrideAttrs (_: { inherit src; });
```

Don’t be thrown off by the `src`. That essentially reads as: `{src = src}`. Adding in our plugins with this extra wrapper function:

```
configure.packages.myVimPackage.start = with prev.vimPlugins; [
    # Overwriting plugin sources with different version
    (withSrc telescope-nvim inputs.telescope-src)
    (withSrc cmp-buffer inputs.cmp-buffer)
    (withSrc nvim-cmp inputs.nvim-cmp)
    (withSrc cmp-nvim-lsp inputs.cmp-nvim-lsp)
    # Plugins from nixpkgs
    lsp_signature-nvim
    lspkind-nvim
    nerdcommenter
    nvim-lspconfig
    plenary-nvim
    popup-nvim
    # Compile syntaxes into treesitter
    (prev.vimPlugins.nvim-treesitter.withPlugins (plugins: with plugins; [ tree-sitter-nix tree-sitter-rust ]))
];
```

Treesitter is an odd case. For those unfamiliar, tree-sitter provides syntax highlighting among a series of other convenient features. There is some useful documentation [here](https://github.com/NixOS/nixpkgs/blob/master/doc/languages-frameworks/vim.section.md#tree-sitter) that we can start with. The available grammar list lives [here](https://github.com/NixOS/nixpkgs/tree/master/pkgs/development/tools/parsing/tree-sitter/grammars).

[## Treesitter expression](https://justin.restivo.me/posts/2021-10-24-neovim-nix.html#treesitter-expression)
----------

Let’s walk through how one might figure out how this `nvim-treesitter` expression works. The specific expression I’m thinking of is:

```
(pkgs.vimPlugins.nvim-treesitter.withPlugins (
  plugins: with plugins; [tree-sitter-nix tree-sitter-python tree-sitter-c tree-sitter-rust]
))
```

The first thing we must do is figure out what `nvim-treesitter.withPlugins` is. We may do this by searching it in nixpkgs: `nix edit nixpkgs#vimPlugins.nvim-treesitter.withPlugins`. This searches the `nixpkgs` flake (which should be present in the registry when flakes are enabled. Think of the registry as a local cache of nixpkgs that exists exactly for this sort of thing). The resulting expression:

```
# Usage:
# pkgs.vimPlugins.nvim-treesitter.withPlugins (p: [ p.tree-sitter-c p.tree-sitter-java ... ])
# or for all grammars:
# pkgs.vimPlugins.nvim-treesitter.withPlugins (_: tree-sitter.allGrammars)
nvim-treesitter = super.nvim-treesitter.overrideAttrs (old: {
  passthru.withPlugins =
    grammarFn: self.nvim-treesitter.overrideAttrs (_: {
      postPatch =
        let
          grammars = tree-sitter.withPlugins grammarFn;
        in
        ''
          rm -r parser
          ln -s ${grammars} parser
        '';
    });
});
```

Let’s proceed line by line. `super.nvim-treesitter.overrideAttrs` is applying an overlay that effectively modifies the already defined `nvim-treesitter` package by overriding something about the “way” it is built (this is called a derivation). As before, `overrideAttrs` takes in a function that defines a set of attributes that “overrides” the pre-existing set of attributes and sets them to new values. Sort of like how with subtyping polymorphism applied to OOP, a child class “inherits” methods from its parent, but may (in some languages at least, notably Java) override them.

In this case, this function defines which attributes to override. `old` is the old set of attributes. The derivation sets the `passthru` attribute which (complexity aside) at a high level allows us to set the plugins list with the syntax above. For more info see [here](https://discourse.nixos.org/t/how-to-merge-several-derivation-outputs-for-plugin-system/537/2).

Check out `3_custom_plugin`. Sometimes plugins may not be added into `nixpkgs`. One example is the theme I like, `darcula`. Luckily, `nix` makes it easy to build plugins:

```
(pkgs.vimUtils.buildVimPluginFrom2Nix { pname = "dracula-nvim"; version = "master"; src = dracula-nvim; })
```

This uses a builtin `vim` plugin builder. Most of the time, we just need to name the plugin, specify its version and source (which is an input). Generally this should build whichever plugin without much extra configuration. Note that to see more documentation `nix edit nixpkgs#vimUtils.buildVimPluginFrom2nix` works quite nicely.

Check out `4_lsp`. We’ve already added all the plugins we need. Now all we need to do is (1) add the LSPs (and other system dependencies) we might need and (2) include configuration as plaintext. The former is done by filling out the `extraRuntimeDeps` attribute:

```
extraRuntimeDeps = with pkgs; [ripgrep clang rust-analyzer inputs.rnix-lsp.defaultPackage.x86_64-linux];
```

Note that we need ripgrep for telescope, clang for tree-sitter, and we are building `rnix-lsp` from source. All with very little effort!

I’ve just pasted what I would normally use to configure `neovim` into `neoVimConfig`. This lives in neoVimConfig, along with keybinds.

Note: The `extraRuntimeDeps` is something I added. I ended up forking the underlying nixpkgs builder into my `DSL` repo because I could not figure out how to pass runtime dependencies onto the path. Ideally, one wants to modify the `PATH` variable to include the dependencies such as ripgrep. Sadly there does not seem to be an easy way to do this, so I added `extraRuntimeDeps` as an argument to do this. `extraRuntimeDeps` get passed to the [`wrapProgram` bash function](https://github.com/NixOS/nixpkgs/blob/master/pkgs/build-support/setup-hooks/make-wrapper.sh#L132), which allows an easy way for us to prepend (in this case, anyway) packages to our path.

Check out `5_ci`. The last thing to do is enable a cache so each machine we pull down to does not go under load. The way to do this is to use a github action to build neovim and push it to github. It is trivial to copy `.github/workflows/nix.conf`. After copying, one must create their own [`cachix` account](https://www.cachix.org/), obtain a key to their cache, and set the `CACHIX_AUTH_TOKEN` github action secret to that key. Then, github actions will be able to push neovim build artifacts (notably language servers, ripgrep, and neovim itself) to this binary cache. Then client-side when we `nix run $NEOVIM_CONFIG`, `nix` will pull directly from this cache.