---
layout: post
title: Bash to Fish Shell
---
I've recently switched back to [fish](http://fishshell.com/) from bash, and
been pretty happy with the change. Fish provides a variety of additional
features over bash, but its main benefit is ease of use. Despite trying several
recommended setups with zsh and bash, I've found fish's auto complete to fit my
needs the best.

![fish shell](/images/fish.png)

Getting `fish` setup on your machine is fairly straightforward. If you're on OS
X, I've found the easiest approach is using [homebrew](http://brew.sh/). You
can install `fish` by running the following command:

` brew install fish `

I would then recommend setting up
[oh-my-fish](https://github.com/bpinto/oh-my-fish), which provides several
useful plugins and themes. Installing `oh-my-fish` can be done by running:

` curl -L https://github.com/bpinto/oh-my-fish/raw/master/tools/install.fish |
fish `

In order to migrate your `~/.bashrc` file to `~/.config/fish/config.fish`,
you'll need to update some of your syntax.

`export GOPATH=$HOME/dev/go` -> `set -x GOPATH $HOME/dev/go`

`source ~/.shenv` -> `. ~/.shenv`
