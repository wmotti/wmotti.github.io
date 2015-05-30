---
layout: post
comments: true
title: Setup ctags for Ruby development
tags: ctags ruby Vim git
---

Reminder to myself: how to setup [ctags](http://ctags.sourceforge.net)
for Ruby development in Vim, to keep updated tags files for projects,
gems and Ruby standard library.

***

Project tags
------------

### Setup git to regenerate ctags index when working tree changes

Create `~/.git_template/hooks/ctags` and mark it as executable:

    #!/bin/sh
    set -e
    PATH="/usr/local/bin:$PATH"
    dir="`git rev-parse --git-dir`"
    trap 'rm -f "$dir/$$.tags"' EXIT
    git ls-files | ctags --tag-relative -L - -f"$dir/$$.tags" --languages=-javascript,sql
    mv "$dir/$$.tags" "$dir/tags"

Create `post-commit`, `post-merge` and `post-checkout` hooks with the same
content:

    #!/bin/sh
    .git/hooks/ctags >/dev/null 2>&1 &

Create a `post-rewrite` hook:

    #!/bin/sh
    case "$1" in
      rebase) exec .git/hooks/post-merge ;;
    esac

### Setup global hooks templates for git

    git config --global init.templatedir '~/.git_template'
    mkdir -p ~/.git_template/hooks

Now every new project, cloned or created, will have these templates.

For existing repositories, use `git init` to safely copy these
templates in them.

***

Gem tags
--------

### Automatically generate ctags for your gem on installation

Install `gem-ctags` RubyGems plugin to automatically invoke ctags on
gems as they are installed:

    gem install gem-ctags

Prm a one-off indexing of the gems that are already installed:

    gem ctags

Install [bundler.vim](https://github.com/tpope/vim-bundler), so Vim will
be aware of all tags files from all gems in the bundle.

***

Standard library tags
---------------------

Install [rbenv-ctags](https://github.com/tpope/rbenv-ctags) rbenv plugin to
automatically generate new indices when a new Ruby interpreter is
installed via rbenv.

    mkdir -p ~/.rbenv/plugins
    git clone git://github.com/tpope/rbenv-ctags.git ~/.rbenv/plugins/rbenv-ctags
    rbenv ctags

Install [vim-ruby](https://github.com/vim-ruby/vim-ruby) and
[vim-rbenv](https://github.com/tpope/vim-rbenv), so Vim will use tags files in
the Ruby `$LOAD_PATH`.

Optionally, install
[rbenv-default-gems](https://github.com/sstephenson/rbenv-default-gems)
to automatically install `gem-ctags` for every new Ruby version. Put it at
the top of `~/.rbenv/default-gems` so that it indexes all gems underneath
it.

***

References:

 * Tim Pope's excellent [Effortless ctags with git](http://tbaggery.com/2011/08/08/effortless-ctags-with-git.html)

 * Arjan van der Gaag's [Combining Vim and Ctags](http://arjanvandergaag.nl/blog/combining-vim-and-ctags.html)

