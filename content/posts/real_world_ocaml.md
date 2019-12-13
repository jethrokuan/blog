+++
title = "Real World OCaml: A Review"
author = ["Jethro Kuan"]
lastmod = 2019-12-13T20:18:52+08:00
draft = false
math = true
+++

Real World OCaml is peppered with interesting tidbits about the
implementations of OCaml that help with understanding the way the
language is constructed.

Here's a quote about the limitations of pattern matching, which
helped my understand the deliberation behind its constraints.

> You can think of patterns as a specialized sublanguage that can
> express a limited (though still quite rich) set of conditions. The
> fact that the pattern language is limited turns out to be a good
> thing, making it possible to build better support for patterns in the
> compiler. In particular, both the efficiency of match statements and
> the ability of the compiler to detect errors in matches depend on the
> constrained nature of patterns.
