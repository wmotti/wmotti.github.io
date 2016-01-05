---
layout: post
comments: true
title: Enable 256 colors in tmux
tags: tmux
---

How to get proper 256 colors support in [tmux](https://tmux.github.io)?

First, be sure your terminal supports 256 colors:

    echo $TERM

It should return 'screen-256color' or 'xterm-256color'.
Then add the following line to your shell configuration file (for example .bashrc):

    set -g default-terminal "screen-256color"

You're done!
