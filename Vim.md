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

This methodology is embodied well in this famous StackOverflow answer: [Your problem with Vim is that you don't grok vi.](https://stackoverflow.com/a/1220118/1422582)

Just like any workflow, Vim requires making small changes to learn. Like learning any other skill, you start out as a slow uncomfortable clumsy beginner, but with practice you can develop proficiency, speed, and more abilities.

The following pages discuss this well with details:

* [Learn Vim Progressively - Yann Esposito](https://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
* [How To Learn Vim: A Four Week Plan - Pete Jang](https://peterxjang.com/blog/how-to-learn-vim-a-four-week-plan.html)
* [Vim Command Workflow - Max Shen](https://m4xshen.me/posts/vim-command-workflow/)

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

You'll find many "distributions" of Vim like SpaceVim, LazyVim, Janus, spf13, or Spacemacs (which is actually Emacs setup to behave like Vim) but I recommend not using these.

They fill Vim with settings and plugins that often defeat the intention of the editor. Plus it's a pain to have to setup new stuff on every system you interact with.

It is better to learn Vim fundamentals with few modifications first, then once you are familiar with Vim as an editor, pick few plugins (if any) to enchance your workflow even more.

### Vim or Neovim?

As a beginner, there is no huge difference between recent Vim 8 or 9 and Neovim.

This page is written to work with either. I'm running Neovim but my config still works fine, even with old Vim 7.

However, if you choose Neovim, be sure to setup its config file as per: [`:help nvim-from-vim`](https://neovim.io/doc/user/nvim.html#nvim-from-vim)

## vimrc

The vimrc file (stored at `~/.vimrc`) is your settings file. It controls the behaviour of the editor on launch.

You'll find many people's settings files on the internet, but here are some things I like in mine.

I suggest to keep vimrc small. Every time mine gets more than a page or two of terminal text (maximized), I trim it down to stuff I don't really need.

### General Behaviour

~~~vim
""" general
set autoindent       " indent the same amount as the previous line on CR
set cindent          " C-style indenting
set noerrorbells     " BEEP (for DOS vim)
set nofoldenable     " disable folding
set formatoptions-=c " stop comments wrapping at textwidth (:help fo-table)
set hidden           " allow moving to another buffer without saving
set hlsearch         " highlight search results
set incsearch        " incremental search as you type
set linebreak        " don't wrap text in the middle of a word
set listchars=tab:>\ ,eol:$,trail:-,extends:>,precedes:<,nbsp:+ "
set modeline         " https://vim.fandom.com/wiki/Modeline_magic
set number           " show line numbers
set relativenumber   " enable hybrid line numbers
set scrolloff=1      " number of lines to keep visible when scrolling
set title            " show title in console
set smarttab         " tab on blank line inserts a shiftwidth, backspace deletes
set splitbelow       " start splits below the current window
set splitright       " start splits to the right of the current window
set wildmenu         " command autocompletion menu (try :color <Tab> to see)

set expandtab        " expand tabs to spaces
set tabstop=4        " consider 4 spaces to be a tab
set shiftwidth=4     " when < or > shifting, move to 4-space boundaries
" when halfway thru spacing and you hit tab, end at (shiftwidth) gaps
if has('softtabstop') | set softtabstop=-1 | endif
~~~

### Theme

I use [Solarized Dark](https://github.com/altercation/vim-colors-solarized) for everything:

~~~vim
""" theme
" https://github.com/altercation/vim-colors-solarized
set background=dark
colorscheme solarized
~~~

If you can't be bothered setting all that up and just want default Vim to not look so bad, consider the `slate` color scheme. This is a nice theme and looks the same in 256-color terminals and truecolor terminals, so you don't have to apply terminal hacks or mess around with truecolor in tmux or anything else like that:

~~~vim
colorscheme slate
~~~

You can find themes on [vimcolorschemes](https://vimcolorschemes.com/). Some popular ones are [gruvbox](https://github.com/morhetz/gruvbox), [everforest](https://github.com/sainnhe/everforest), and [onedark](https://vimcolorschemes.com/joshdick/onedark.vim).

If you find your theme looks bad, you might need to `set termguicolors` (some themes needs this, some don't), or make sure your [terminal supports truecolor](https://unix.stackexchange.com/questions/404414/print-true-color-24-bit-test-pattern), or [override `Tc` in tmux](https://stackoverflow.com/questions/41783367/tmux-tmux-true-color-is-not-working-properly).

### Stop Using the Arrow Keys

Repeatedly pressing the arrow keys to navigate is an anti-pattern. To force yourself to learn motions, disable the arrow keys:

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

Once you are ready for full immersion and want repeated presses of the `hjkl` directions disabled too, try [vim-hardtime](https://github.com/takac/vim-hardtime).

### Disable Mouse

I don't want the mouse to be active in my terminal Vim sessions:

~~~vim
" disable mouse
set mouse=           " disable mouse
~~~

### Graphical Copy/Paste

Vim yanks and pastes work in its own set of clipboard-like things called "registers".

However, it is useful to interact with the system clipboard. Editing big swathes of browser text area in Vim is particularly helpful. These rely on the presence of `xclip` command:

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

If you're running very recent Vim or Neovim, you don't even need this, you can just yank and paste to/from the system clipboard directly:

~~~vim
if has("unnamedplus")
    set clipboard=unnamedplus
else
    set clipboard=unnamed
endif
~~~

### Statusline

There are many statusline plugins - [powerline](https://github.com/powerline/powerline), [lightline](https://github.com/itchyny/lightline.vim), [airline](https://github.com/vim-airline/vim-airline) - but I don't find any of them necessary. The below is a sufficient emulation of lightline for my needs.

Note, this could easily be done all in one big command, but annotating it out over multiple additions to `statusline+=` makes human maintenance easier

~~~vim
""" statusline
set laststatus=2    " always show the statusline
set showmode        " show mode line ---INSERT---
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

I've actually published this as a plugin if you prefer that: <https://github.com/superjamie/zeroline.vim>

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
" clear last search pattern, removing search highlights
nnoremap <leader>h :let @/ = ""<cr>
" toggle list characters
nnoremap <leader>l :set list!<CR>:set list?<CR>
" toggle line numbers
nnoremap <leader>n :set relativenumber!<CR>:set number!<CR>
" toggle paste mode
nnoremap <Leader>p :set paste!<CR>:set paste?<CR>
" toggle relative line numbers
nnoremap <leader><leader> :set relativenumber!<CR>
" remove trailing whitespace through whole document
nnoremap <leader>w :%s/\s\+$//<CR>:match<CR>:nohl<CR> :<Esc>
" re-indent whole file (mm creates mark m, gg=G indents, tick m goes to mark m
map <Leader>= mmgg=G`m
~~~

### Splits

You can split windows with `Ctrl+w` then `v` (vertical split) and/or `Ctrl+w` then `s` (split horizontal).

Move around splits with `Ctrl+w` and one of the `hjkl` directions, or switch to the next split quickly with `Ctrl+w` twice.

Close a split with `Ctrl+w` then `q` or even `:q`. Close all *other* splits with `Ctrl+w` then `o` or `:only`

If you find you've opened a split in the wrong horizontal/vertical orientation, you can move splits around with `Ctrl+w` then the `HJKL` direction keys (capitals, so use `Shift`)

### Buffers

You can open multiple files in Vim, and those files are stored in "bufffers".

Your current window displays a view of a buffer, and you can switch back and forth to other buffers.

Here are some handy keybinds for using bufffers:

~~~vim
" display list of buffers
noremap <leader>b :buffers<cr>
" close current buffer without closing split, switches to b# (previous buffer)
nnoremap <leader>B :b#<bar>bd#<CR>
" from vim-unimpaired
noremap [b :bprev<CR>
noremap ]b :bnext<CR>
noremap [B :bfirst<CR>
noremap ]B :blast<CR>
~~~

If you'd like to learn more about Vim's concepts of Window, Buffer, Tab, check:

<https://vim.fandom.com/wiki/Buffers>

~~~
:help window

Summary:
   A buffer is the in-memory text of a file.
   A window is a viewport on a buffer.
   A tab page is a collection of windows.
~~~

I don't use tabs.

----

## Plugins

I know I said not to use many plugins, but these are the few I do use.

You will see mention of "plugin managers" like Pathogen or Vundle, but you don't need these anymore, Vim has native plugin management now.

Add plugins into `~/.vim/pack/NAME/start/` where `NAME` is your name or a group of plugins or just `plugins` if you aren't fussed.

You can use the `~/.vim/pack/NAME/opt/` directory for plugins which don't load automatically, you can add them later during runtime with `:packadd plugin-name`

### vim-sneak

<https://github.com/justinmk/vim-sneak>

My number one plugin and the only thing I really insist on having with me.

You'll learn the motions `f` to go "forward" to text (or `F` to do the opposite direction), and `t` to change/delete "to" something (or `T` to do the opposite direction).

Following our first example again:

~~~
    █printf("Hello, world!\n");
~~~

I could move to the open bracket with `f(` meaning "forward to first open bracket".

I could also change the word `printf` with `ct(` meaning "change to open brace".

However, when you have multiple possible matches it becomes a little more difficult to move exactly where you want.

sneak adds motions `s` (forward) and `S` (back) which match **two** characters.

So again with our example, say I wanted to move to the `ll` in "Hello", sneak lets me type `sll`.

It also brings up a third highlighted jump if you have multiple matches at two letters.

This is so good it should be part of Vim!

### buftabline

<https://github.com/ap/vim-buftabline>

When opening multiple files, this places the files in a horizontal numbered list at the top of the screen, just like tabs in other editors.

### Fugitive

<https://github.com/tpope/vim-fugitive>

Adds git capabilities to Vim.

Most common commands can be prefixed with `:Git` (or just `:G`) such as `log` or `diff` or `add` or `commit`, it picks up all your aliases in `~/.gitconfig` too.

It also adds Vim-awareness to these. For example, the `log` or `log --oneline` opens the log in a buffer which you can navigate. Press `o` to open a full commit in a new split, or `Enter` to use the log window. Go back/forward with `Ctrl+o` and `Ctrl+i` (Vim's native history).

My job is almost entirely to read code and understand the history of a commit. Fugitive's `:Git blame` view is great for this! Particularly how it lets you re-blame on a parent commit with `~` key.

### polyglot

<https://github.com/sheerun/vim-polyglot>

The built-in syntax highlighting is pretty good, but it can be better.

This adds lots of better syntax highlighting, and it only loads when needed so it doesn't slow down Vim for filetypes you never use.

### Language Server Protocol (LSP)

A bit beyond the scope of this document, but if you're a programmer and want fancy language awareness like a real IDE, this provides it.

I have found [`vim-lsp`](https://github.com/prabirshrestha/vim-lsp) to be the easiest to get working.

Look around for the best language server for your programming languages, try a few, there are many listed in [vim-lsp-settings](https://github.com/mattn/vim-lsp-settings).

For C programming I use [ccls](https://github.com/MaskRay/ccls/wiki/vim-lsp).

The suggested keybinds are pretty good and very Vim-like. I change the hover scroll because I use `Ctrl+f` to go forward, and I add a rename on `F2`:

```vim
    nmap <buffer> gd <plug>(lsp-definition)
    nmap <buffer> gs <plug>(lsp-document-symbol-search)
    nmap <buffer> gS <plug>(lsp-workspace-symbol-search)
    nmap <buffer> gr <plug>(lsp-references)
    nmap <buffer> gi <plug>(lsp-implementation)
    nmap <buffer> gt <plug>(lsp-type-definition)
    nmap <buffer> <leader>rn <plug>(lsp-rename)
    nmap <buffer> [g <plug>(lsp-previous-diagnostic)
    nmap <buffer> ]g <plug>(lsp-next-diagnostic)
    nmap <buffer> K <plug>(lsp-hover)
    nnoremap <buffer> <expr><c-k> lsp#scroll(+4)  "" changed
    nnoremap <buffer> <expr><c-j> lsp#scroll(-4)  "" changed
    nmap <buffer> gD <plug>{lsp-declaration)  "" added
    nmap <buffer> <f2> <plug>(lsp-rename)  "" added
```

### Auto-Completion

Vim has auto-completion of words in the current file with `Ctrl+n`. This works in any filetype, even plain text.

When using LSP (technically, when using something which sets `omnifunc`) you can open the Omni auto-completion menu in Insert Mode with `Ctrl+x Ctrl+o`.

If you want `Tab` to autocomplete like a normal IDE, install the [supertab](https://github.com/ervandew/supertab) plugin, then in the same place as the above LSP keybinds, add:

```vim
    if exists("loaded_supertab") | call SuperTabSetDefaultCompletionType("<c-x><c-o>") | endif
```

See `:help ins-completion` for a larger explanation of Vim's auto-complete capabilities and the entire separate `Ctrl-x` sub-mode of Insert Mode.

----

## Other Favorite Tips and Tricks

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

### Terminal Mode

If you regularly copy/paste things to/from terminals, you don't need a separate terminal window, recent Vim and Neovim have a terminal buffer type.

Enter it with `:terminal`.

You can open a terminal in a split with `:split +terminal` or `:vert split +terminal`

If this is a thing you do all the time, you might like these keybinds:

```vim
nnoremap <leader>t :vsp +term<cr>
nnoremap <leader>T :sp +term<cr>
```

### Temporary Normal Mode

If you're in Insert Mode and you need to run just one quick command in Normal Mode, you can press `Ctrl+o` to temporarily exit Insert.

The mode print down the bottom will change from `-- INSERT --` to `-- (insert) --` to show you the mode change.

If you do something which takes you away from the current buffer, you stay in Normal mode.

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
