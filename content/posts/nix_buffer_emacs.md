+++
title = "Using nix-buffer with Emacs"
author = ["Jethro Kuan"]
lastmod = 2019-12-13T20:20:30+08:00
draft = false
math = true
+++

I do [a lot of note-taking](https://braindump.jethrokuan.com/) in Emacs, and have recently started using
org-babel within my notes. Being on NixOS, this proved to be slightly
problematic: `org-babel` requires the executables to be in `PATH`. In
NixOS this is concerning: we don't want the executables to be
available globally.

My traditional approach would be to use the [direnv](https://direnv.net/) [integration](https://github.com/shosti/direnv-mode) in
Emacs, populating my path in a certain directory. However, in this
case I keep my notes in a flat hierarchy:

```org
/home/jethro/.org/braindump/org/
├── artificial_intelligence.org
├── auto
├── bayesian_inference.org
├── bittorrent.org
├── blockchain.org
├── cite
├── coding_interview.org
├── computer_organization.org
├── computer_vision.org
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
