+++
title = "Using nix-buffer with Emacs"
author = ["Jethro Kuan"]
lastmod = 2019-01-16T09:20:39+08:00
tags = ["emacs"]
draft = true
+++

I do [a lot of note-taking](https://braindump.jethrokuan.com/) in Emacs, and have recently started using
org-babel within my notes. Being on NixOS, this proved to be slightly
problematic: `org-babel` requires the executables to be in `PATH`. In
NixOS this is concerning: we don't want the executables to be
available globally.

My traditional approach would be to use the [direnv](https://direnv.net/) [integration](https://github.com/shosti/direnv-mode) in
Emacs, populating my path in a certain directory. However, in this
case I keep my notes in a flat hierarchy:

```shell
tree -L 1 -P "*.org" ~/.org/braindump/org/ | head -n 10
```

In this case `direnv` doesn't let me load different environments for
different files. Here I turn to `nix-buffer`, which by default loads a
`dir-locals.nix` file of this form:

```nix
let pkgs = import <nixpkgs> {}; in
  pkgs.nixBufferBuilders.withPackages [ pkgs.rWrapper ]
```

To make it load a specific Nix file per org-file, all that's left is
to set a file-local variable for `nix-buffer-root-file`. And that's it!
