---
layout: post
title: "Lint your shell scripts"
---

I will start this by quoting the [bashstyle][bashstyle]'s readme:

> Bash is like the JavaScript of systems programming. Although in some cases
> it's better to use a systems language like C or Go, Bash is actually an ideal
> systems language for many smaller POSIX-oriented or command line tasks.
> Here's three quick reasons why:
>
> - It's everywhere. Like JavaScript for the web, Bash is already there ready
> for systems programming.
> - It's neutral. Unlike Ruby, Python, JavaScript, or PHP, Bash offends equally
> across all communities. ;)
> - It's made to be glue. Write complex parts in C or Go (or whatever!), and
> glue them together with Bash.

My concern about that is the quality of the code itself. Like JavaScript,
most people will just Google and do what they want in the first way that they
found - _quick and dirty_. You can blame me too.

So, projects like [bashstyle][bashstyle] are important to set a common sense
in how to do things using bash. The problem is that it's not automated.

A project that really helps with that is [shellcheck][shellcheck]. It's an
executable written in Haskell, which can lint your scripts (in bash, zsh, and
others). Sure enough, we can put this in a Continuous Integration system and
watch it do the validation for us.

To make it easy to integrate [shellcheck][shellcheck] and
[travis-ci](http://travis-ci.org), I created a project called
[shell-travis-build](https://github.com/caarlos0/shell-travis-build). It is
intended to be added as a submodule, like this:

```bash
git submodule add https://github.com/caarlos0/shell-travis-build.git build
cp build/travis.yml.example .travis.yml
```

Travis will always clone a project with its submodules before the build, so,
it will always work. :beer:

I'm already using this in my [dotfiles][dotfiles], and found some really stupid
mistakes to fix. Sure thing, this is an awesome tool!

Wanna see it in the so said _real world_? Check my [dotfiles][dotfiles]
`build.sh` and `travis.yml` files.

Happy hacking!

[bashstyle]: https://github.com/progrium/bashstyle
[shellcheck]: https://github.com/koalaman/shellcheck
[dotfiles]: https://github.com/caarlos0/dotfiles
