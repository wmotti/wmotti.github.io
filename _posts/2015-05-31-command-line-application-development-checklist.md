---
layout: post
comments: true
title: Command-line application development checklist
tags: ruby cli testing
---

 1. define the interface

    1.1 define a clear and concise purpose

    1.2 choose between a simple command-line application and a command suite

    1.3 define options, arguments and commands

      * single command-line app: options without arguments (switches), options with arguments (flags), arguments

      * command suite: global options (with and without arguments), commands, command options (with and without arguments) and arguments

    1.4 use short-form, long-form and negatable long-form options

    1.5 choose default values for flags and arguments

      * make common tasks easy

      * make uncommon tasks possibile (but not easy)

      * make default behavior nondestructive

    1.6 validate arguments to flags

 2. code

    2.1 choose a library (or roll your own)

      * single command-line app: [OptionParser](http://ruby-doc.org/stdlib/libdoc/optparse/rdoc/OptParse.html), [trollop](http://trollop.rubyforge.org/), [methadone](http://naildrivin5.com/methadone/), [main](https://github.com/ahoward/main), ...

      * command suite: [GLI](http://naildrivin5.com/gli/), [main](https://github.com/ahoward/main), [thor](http://whatisthor.com/), ...

    2.2 structure the code tree following standard Ruby conventions (lib, ...)

    2.3 apply OO design principles and patterns (wisely)

 3. add configurability

    3.1 use a YAML-based configuration in a dotted `.rc` files placed in the user's home directory

    3.2 create configuration file at startup, if missing, and notify the user

 4. embrace interoperability conventions

    4.1 use the standard input and the standard error streams appropriately ([Open3](http://ruby-doc.org/stdlib/libdoc/open3/rdoc/Open3.html), STDOUT, STDERR, $stdout, $stderr)

    4.2 use the standard input stream as the default source for input

    4.3 use standard exit codes to report success or failures

    4.4 provide pretty-print and machine formatting options, choose the default and switch based on the context ([STDOUT.tty?](http://ruby-doc.org/core/IO.html#method-i-tty-3F))

    4.5 trap signals sent from other apps

    4.6 name files uniquely and in common locations (such as `/tmp`) to avoid collisions

    4.7 do not delete or overwrite files as a side effect without explicit instructions from the user

 5. add documentation

    5.1 don't forget the inline help (`-h` or `--help`)

    5.2 add a short description in the banner

    5.3 explain options and arguments (and commands for command suites)

    5.4 include a conventionally structured man page via [gem-man](http://defunkt.io/gem-man/) and [ronn](http://rtomayko.github.com/ronn/)

    5.5 generate documentation in the [Rdoc](http://docs.seattlerb.org/rdoc/) format

 6. test

    6.1 apply an outside-in test strategy

    6.2 test user behavior with acceptance tests using [Cucumber](https://cucumber.io/) + [Aruba](https://github.com/cucumber/aruba)

    6.3 test in isolation with unit tests using [minitest](http://docs.seattlerb.org/minitest/)

    6.4 use test doubles, if needed, with [mocha](http://gofreerange.com/mocha/docs/), [construct](https://github.com/devver/construct), [FakeFS](https://github.com/defunkt/fakefs), ...

 7. final touches

    7.1 add tab-completion if possible (bash, etc)

    7.2 add color to the output with [rainbow](https://github.com/sickill/rainbow), [paint](https://github.com/janlelis/paint), [term-ansicolor](https://flori.github.io/term-ansicolor/), ...

    7.3 format output as tables, if useful, using [terminal-tables](https://github.com/tj/terminal-table), [command_line_reporter](https://github.com/wbailey/command_line_reporter), [formatador](https://github.com/geemus/formatador), ...

    7.4 enhance the output with [formatador](https://github.com/geemus/formatador), [progress_bar](https://github.com/paul/progress_bar), ...

    7.5 provide interactive user input with [readline](http://ruby-doc.org/stdlib/libdoc/readline/rdoc/Readline.html)

 8. distribution

    8.1 choose a distribution method: [RubyGem](http://guides.rubygems.org/rubygems-basics/), rpm with [gem2ruby](https://github.com/fedora-ruby/gem2rpm), ...

    8.2 manage dependencies with [gemspec](http://guides.rubygems.org/specification-reference/), [bundler](http://bundler.io/), ...

***

References:

 * the awesome book
   [Build Awesome Command-Line Applications in Ruby 2](https://pragprog.com/book/dccar2/build-awesome-command-line-applications-in-ruby-2) by [David Copeland](http://naildrivin5.com/), published by [The Pragmatic Programmers, LLC](http://www.pragprog.com)
