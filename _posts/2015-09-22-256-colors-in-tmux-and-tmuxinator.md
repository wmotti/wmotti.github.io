---
layout: post
comments: true
title: 256 colors in tmux and tmuxinator
tags: tmux tmuxinator
---

Aliases I need to setup in .bashrc to enable 256 colors in
[tmux](https://tmux.github.io) and
[tmuxinator](https://github.com/tmuxinator/tmuxinator):

    alias tmux='TERM=xterm-256color tmux -2'
    alias tmuxinator='TERM=xterm-256color tmuxinator'
    alias mux='TERM=xterm-256color mux'

YMMV. If you know a better way to get the same result, please tell me :wink:
