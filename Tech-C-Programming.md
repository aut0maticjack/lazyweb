I like C. You don't have to, but I do.

Here are some useful/interesting/insightful resources which I always refer back to:

* [How to C in 2016](https://matt.sh/howto-c)
* [Linux Kernel coding style](https://www.kernel.org/doc/Documentation/process/coding-style.rst) and [linuxsty.vim](https://github.com/vivien/vim-linux-coding-style)
* [Programming Articles by Adam Tornhill](https://www.adamtornhill.com/articles.htm)
* [Google C++ Style Guide - Names and Order of Includes](https://google.github.io/styleguide/cppguide.html#Names_and_Order_of_Includes)

Other things I liked:

* [Higher-Level C by ERJH](https://ejrh.wordpress.com/higher-level-c/)
    * [Objects in C](https://ejrh.wordpress.com/2011/03/31/objects-in-c/)
    * [Encapsulation in C](https://ejrh.wordpress.com/2011/04/29/encapsulation-in-c/)
    * [Method Polymorphism in C](https://ejrh.wordpress.com/2011/09/10/method-polymorphism-in-c/)
    * [Namespaces in C](https://ejrh.wordpress.com/2012/01/24/namespaces-in-c/)
* [Seventeen steps to safer C code by Thomas Honold](https://www.embedded.com/seventeen-steps-to-safer-c-code/)
* [The Ultimate Question of Programming, Refactoring, and Everything](https://pvs-studio.com/en/blog/posts/cpp/0391/)
    * [How to make fewer errors at the stage of code writing. Part N1](https://pvs-studio.com/en/blog/posts/cpp/a0070/)
    * [How to make fewer errors at the stage of code writing. Part N2](https://pvs-studio.com/en/blog/posts/cpp/a0072/)
* [How I Program C by Eskil Steenberg](https://www.youtube.com/watch?v=443UNeGrFoM)

Building

* <https://raw.githubusercontent.com/superjamie/snippets/master/Makefile>
* <https://raw.githubusercontent.com/superjamie/snippets/master/Makefile-simple>

Arguments

* [GNU getopt](https://www.gnu.org/software/libc/manual/html_node/Getopt.html)
* [docopt - Command-line interface description language](http://docopt.org/)

Learning

* <https://learn-c.org/>
* [CodeStepByStep - C Exercises](https://www.codestepbystep.com/problem/list/c)

Networking

* [Beej's Guide to Network Programming](http://beej.us/guide/bgnet/)

SDL

* [SDL Wiki](https://wiki.libsdl.org/)
* [TwinklebearDev SDL 2.0 Tutorial](https://www.willusher.io/pages/sdl2/) (C++ but explains concepts)
* [Lazy Foo' Productions - Beginning Game Programming v2.0](https://lazyfoo.net/tutorials/SDL/)

Roguelike Stuff

* [libtcod](https://github.com/libtcod/libtcod)
* [BearLibTerminal](http://foo.wyrd.name/en:bearlibterminal)

Rust

* [Rust By Example](https://doc.rust-lang.org/stable/rust-by-example/)
* [The Rust Programming Language](https://doc.rust-lang.org/book/)

DOS

* <https://delorie.com/djgpp/>
* <https://github.com/andrewwutw/build-djgpp>
* <https://pdcurses.org/>
* <https://github.com/msikma/allegro-4.2.2-xc>

## Vim

### vim-lsp

<https://github.com/prabirshrestha/vim-lsp>

This is rad for everything except the kernel.

I use the [ccls](https://github.com/MaskRay/ccls/wiki/vim-lsp) language server, I've found it better than clangd.

I generate `compile_commands.json` with [bear](https://github.com/rizsotto/Bear) like `bear -- make`

Key bindings:

```vim
    setlocal signcolumn=no
    if exists('+tagfunc') | setlocal tagfunc=lsp#tagfunc | endif
    nmap <buffer> gd <plug>(lsp-definition)
    nmap <buffer> gs <plug>(lsp-document-symbol-search)
    nmap <buffer> gS <plug>(lsp-workspace-symbol-search)
    nmap <buffer> gr <plug>(lsp-references)
    nmap <buffer> gi <plug>(lsp-implementation)  " doesn't seem to do anything for C
    nmap <buffer> gt <plug>(lsp-type-definition)
    nmap <buffer> <leader>R <plug>(lsp-rename)
    nmap <buffer> [g <plug>(lsp-previous-diagnostic)
    nmap <buffer> ]g <plug>(lsp-next-diagnostic)
    nmap <buffer> K <plug>(lsp-hover)
    nnoremap <buffer> <expr><c-k> lsp#scroll(+4)
    nnoremap <buffer> <expr><c-j> lsp#scroll(-4)
    nmap <buffer> <f2> <plug>(lsp-rename)
```

### GNU Global's gtags-cscope

For the Linux kernel, I use the source code tagging system [GNU Global](https://www.gnu.org/software/global/) to generate source code tags (it's much better than ctags), and this ships with a plugin that improves on the old `vim-cscope`:

<https://cvs.savannah.gnu.org/viewvc/global/global/gtags-cscope.vim?revision=1.14&view=markup>

There's a bit of history there, this assumes familiarity with cscope concepts:

* symbol global definition
* symbol usage
* symbol callers
* extended regex search

It creates Vim commands for these:

* `:cs f g SYMBOL`
* `:cs f s SYMBOL`
* `:cs f c SYMBOL`
* `:cs f e PATTERN`

It creates leader actions for these when you're on a keyword:

* Ctrl + leader + g
* Ctrl + leader + s
* Ctrl + leader + c
* Ctrl + leader + e

This is MUCH quicker than constantly hopping in and out of cscope, and lets you use Vim's native jump list commands to navigate older (**Ctrl+o**) and newer (**Ctrl+i**) as you read. See `:help jump-motions`

