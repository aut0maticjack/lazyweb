# Vim

The best text editor (as long as you can manage to [exit it](https://github.com/hakluke/how-to-exit-vim), haha).

## Workflow

Using Vim properly is like speaking a "language" to your text editor.

It requires a change in workflow from "move the cursor and do things manually" to actually expressing what you want to achieve.

The overall idea is that editing becomes more precise and efficient.

For example, given the cursor `█` on the line:

~~~
    █printf("Hello, world!\n");
~~~

If you want to change the text inside the quotes, you could:

* Mouse method: Move the cursor with the mouse to the H, highlight the text inside the quotes, and start typing to replace it. This is undesirable as it requires taking your hand off the keyboard to use the mouse, then putting your hand back on again to type.
* Keyboard method: Use the arrow keys (maybe Ctrl+arrow to jump words), move the cursor to the H, press the Delete key 13 times (or hold Shift and highlight right, perhaps with Ctrl+arrow to jump words), and start typing. This is undesirable as it requires pressing lots of keys, it takes your arrow-key hand away from the alphanumeric typing keys, different editors might have different behaviour highlighting words and interpreting special characters (the set `()"\`) as parts of words.
* Vim method: Press three keys, `c`hange `i`nside `"` (quotes), and start typing your replacement. This is desirable as it says what you actually wanted to do, behaves consistently and expectedly, and takes very few keypresses to achieve so you can be more productive overall.

Just like any workflow, Vim requires making small changes to learn. Like learning any other skill, you start out as a slow uncomfortable clumsy beginner, but with practice you can develop proficiency, speed, and more abilities.

The following pages discuss this well with details:

* [Learn Vim Progressively - Yann Esposito](https://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
* [How To Learn Vim: A Four Week Plan - Pete Jang](https://peterxjang.com/blog/how-to-learn-vim-a-four-week-plan.html)

You could also watch the Vimcasts and gradually integrate the useful tips into your workflow. Scroll to the bottom of the page for the first one and work your way up:

* <http://vimcasts.org/episodes/archive/>

You can also run `vimtutor` on the commandline to start an interactive tutorial.

### Getting Help

If you are ever stuck, you can search the internet for the thing you want to do, with "vim" added.

Most likely you will find a Stack Overflow or [Vim Tips Wiki](https://vim.fandom.com/) page explaining how to do it.

You might want to browse the Wiki's list of [Best Vim Tips](https://vim.fandom.com/wiki/Best_Vim_Tips)

If you don't know what a command, option, or setting within Vim does, get help with it using `:help thing` `:help :thing`

----

## Environment

You'll find many "distributions" of Vim like Janus, spf13, or Spacemacs (which is actually Emacs setup to behave like Vim) but I recommend not using these.

They fill Vim with settings and plugins that often defeat the intention of the editor. Plus it's a pain to have to setup new stuff on every system you interact with.

It is better to learn Vim fundamentals with few modifications first, then once you are familiar with Vim as an editor, pick few plugins (if any) to enchance your workflow even more.

## vimrc

The vimrc file (stored at `~/.vimrc`) is your settings file. It controls the behaviour of the editor on launch.

You'll find many people's settings files on the internet, but here are some things I like in mine.

I suggest to keep vimrc small. Every time mine gets more than a page of terminal text (maximized), I trim it down to stuff I don't really need.

### General Behaviour

~~~vim
""" general
set autoindent      " indent the same amount as the previous line on CR
set cindent         " C-style indenting
set hidden          " allow moving to another buffer without saving
set hlsearch        " highlight search results
set incsearch       " incremental search as you type
set linebreak       " don't wrap text in the middle of a word
set listchars=tab:>\ ,eol:$,trail:-,extends:>,precedes:<,nbsp:+ " based on vim-sensible
set modeline        " enable modelines
set noerrorbells    " BEEP (mostly useful for DOS Vim)
set number          " show line numbers
set scrolloff=1     " number of lines to keep visible when scrolling
set title           " show title in console
set smarttab        " tab on blankline inserts a shiftwidth, backspace deletes a shifwidth
set splitbelow      " start splits below the current window
set splitright      " start splits to the right of the current window
set wildmenu        " command autocompletion menu
syntax enable       " enable syntax highlighting

set expandtab       " expand tabs to spaces
set tabstop=4       " consider 4 spaces to be a tab
set shiftwidth=4    " when < or > shifting, move to 4-space boundaries
set softtabstop=-1  " when halfway thru spacing and hit tab, end at 4 space gaps (-1 = use shiftwidth)
~~~

### Theme

I use Solarized Dark for everything:

~~~vim
""" theme
" https://github.com/altercation/vim-colors-solarized
set background=dark
colorscheme solarized
~~~

### Stop Using the Arrow Keys

Pepeatedly pressing the arrow keys to navigate is an anti-pattern. To force yourself to learn motions, disable the arrow keys:

~~~vim
" unmap arrow keys
noremap <Up> <NOP>
noremap <Down> <NOP>
noremap <Left> <NOP>
noremap <Right> <NOP>
inoremap <Up> <NOP>
inoremap <Down> <NOP>
inoremap <Left> <NOP>
inoremap <Right> <NOP>
~~~

### Disable Mouse

I don't want the mouse to be active in my terminal Vim sessions:

~~~vim
" disable mouse
autocmd BufEnter * set mouse=
~~~

### Graphical Copy/Paste

However, it is sometimes useful to interact with the clipboard. Editing big swathes of browser text area in Vim is particularly helpful. These rely on the presence of `xclip` command:

~~~vim
" graphical copypaste (requires xclip)
com! -range Xc :silent :<line1>,<line2>w !xclip -selection clipboard -i
ca xc Xc
com! -range Xp :silent :r !xclip -selection clipboard -o
ca xp Xp
~~~

Now you can:

* Paste from the GUI clipboard with `:xp`
* Highlight with Visual mode and copy to GUI clipboard with `:xc`

### Statusline

There are many statusline plugins - powerline, lightline, airline - but I don't find any of them necessary. The below is a sufficient emulation of vim-airline for my needs.

Note, this could easily be done all in one big command, but annotating it out over multiple additions to `statusline+=` makes human maintenance easier

~~~vim
""" statusline
set laststatus=2    " always show the statusline
set showmode        " show mode line ---INSERT---
hi ModeMsg cterm=NONE ctermfg=White
" initialise to blank
set statusline=
" space, buffer number surrounded by [square braces]
set statusline+=\ [%n]
" space, filename (tail)
set statusline+=\ %t
" space, flags: modified, readonly, help, preview
set statusline+=\ %m%r%h%w
" right align
set statusline+=%=
" file format (line endings)
set statusline+=%{&ff}
" space, pipe, space, file encoding
set statusline+=\ \:\ %{''.(&fenc!=''?&fenc:&enc).''}
" space, pipe, space, filetype
set statusline+=\ \:\ %{&ft}
" space, pipe, space, min-3-width percent through file in lines
set statusline+=\ \:\ %2p%%
" space, pipe, space, min-4-width line number
set statusline+=\ \:\ %3l 
" colon, min-2-character left-aligned virtual column number, space
set statusline+=:%-2v\ "
~~~

### Filetypes

You can change Vim's behaviour per filetype, eg:

~~~vim
""" filetypes
augroup configs
    autocmd BufEnter Makefile setlocal noexpandtab
    autocmd BufNewFile,BufReadPost *.ino set filetype=c  " read Arduino sketches as C
    autocmd BufWritePre *.py :%s/\s\+$//e  " strip trailing whitespace from Python files
    autocmd FileType c    setlocal noexpandtab tabstop=8 shiftwidth=8 softtabstop=8
    autocmd FileType cpp  setlocal noexpandtab tabstop=8 shiftwidth=8 softtabstop=8
    autocmd FileType diff setlocal noexpandtab tabstop=8 shiftwidth=8 softtabstop=8
    autocmd FileType xml  setlocal   expandtab tabstop=2 shiftwidth=2 softtabstop=2
augroup END
~~~

### Leader

The leader key is the backslash `\` by default, and can be used for shortcuts:

~~~vim
" remove highlights
nnoremap <leader>h :nohl<CR>:match none<CR>:call clearmatches()<CR> :<Esc>
" toggle list characters
nnoremap <leader>l :set list!<CR>:set list?<CR>
" toggle line numbers
nnoremap <leader>n :set number!<CR>:set number?<CR>
" toggle paste mode
nnoremap <Leader>p :set paste!<CR>:set paste?<CR>
" toggle relative line numbers
nnoremap <leader>r :set relativenumber!<CR>:set relativenumber?<CR>
" reload config
nnoremap <leader>v :source ~/.vimrc<CR>
" remove trailing whitespace through whole document
nnoremap <leader>w :%s/\s\+$//<CR>:match<CR>:nohl<CR> :<Esc>
" re-indent whole file (mm creates mark m, gg=G indents, tick m goes to mark m
map <Leader>= mmgg=G`m
~~~

----

## Plugins

I know I said not to use many plugins, but these are the few I do use:

### buftabline

<https://github.com/ap/vim-buftabline>

When opening multiple files, this places the files in a horizontal numbered list at the top of the screen.

If you'd like to learn more about Vim's concepts of Window, Buffer, Tab, check:

<https://vim.fandom.com/wiki/Buffers>

~~~
:help window

Summary:
   A buffer is the in-memory text of a file.
   A window is a viewport on a buffer.
   A tab page is a collection of windows.
~~~

This plugin moves the bufferlist into the tabline.

### Fugitive

<https://github.com/tpope/vim-fugitive>

Adds git capabilities to Vim. I don't use this to make commits (maybe I should look into that). My job is almost entirely to read code and understand the history of a commit. Fugitive's `:Git blame` view is great for this.

### GNU Global's gtags-cscope

I use the source code tagging system [GNU Global](https://www.gnu.org/software/global/) to generate source code tags (it's much better than ctags), and this ships with a plugin that improves on the old `vim-cscope`:

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

----

## Favorite Tips and Tricks

### z Commands

* `zt` - current line to top of screen
* `zz` - current line to middle of screen
* `zb` - current line to bottom of screen

Useful for browsing around source, or if your search ends up in an uncomfortable reading position.

### Re-indent text

The `=` command re-indents based on the current settings. Useful when loading other people's strange source code (but not for contributing your personal indent preferences back to them).

For example: `ggVG=` (`gg` go to top, `VG` visual select to bottom, `=` re-format)

### Re-format text

The `gq` command re-formats based on the current settings, useful for text wrap settings

* Current line: `gqq` or `gq<CR>`
* Whole document: `ggVGgq`

### Modelines

Modelines are a way you can modify the behaviour of a particular document, say you want a different width for tabs, different wrapping behaviour, etc. The modeline doesn't interfere with the original document, usually by being a source code comment or some other inactive type of line. It is explained full on the wiki, plus some quick examples of modelines below.

<https://vim.fandom.com/wiki/Modeline_magic>

Markdown:

~~~html
<!-- vim: set linebreak textwidth=120 wrap: -->
~~~

C:

~~~c
/* vim: set cindent noexpandtab tabstop=8 shiftwidth=8 softtabstop=8: */
~~~

----

## Todo

I have things I'd like to get better at with Vim too

### Registers 

* https://www.brianstorti.com/vim-registers/
* https://www.tutorialspoint.com/vim/vim_registers.htm
* https://learnvim.irian.to/basics/registers

### Quickfix List and Location List

* https://freshman.tech/vim-quickfix-and-location-list/
* https://vonheikemen.github.io/devlog/tools/vim-and-the-quickfix-list/

### Ex Mode

Right now I just disable it:

~~~vim
map q: <Nop>     " disable command history
nnoremap Q <nop> " disable Ex mode
~~~

* https://superuser.com/questions/22455/what-is-the-ex-mode-for-batch-processing-for
* https://www.jakeworth.com/exit-vim-ex-mode/
* https://vi.stackexchange.com/questions/457/does-ex-mode-have-any-practical-use