# Vim

The best text editor (as long as you can manage to [exit it](https://github.com/hakluke/how-to-exit-vim), haha).

Using Vim properly is like speaking a "language" to your text editor. It requires a change in workflow from "move the cursor here and do things manually" to actually expressing what you want to achieve.

For example, given the cursor `|` on the line:

~~~
  |printf("Hello, world!\n");
~~~

If you want to change the text inside the quotes, you could:

* Mouse method: Move the cursor with the mouse to the H, highlight the text inside the quotes, and start typing to replace it. This is undesirable as it requires taking your hand off the keyboard to type, then putting it back on again.
* Keyboard method: Use the arrow keys (maybe Ctrl+arrow ot jump words), move the cursor to the H, press the Delete key 13 times (or hold Shift and highlight right, perhaps with Ctrl+arrow to jump words), and start typing. This is undesirable as it requires pressing lots of keys, and different editors might have different behaviour highlighting words and interpreting special characters (the set `()"\`) as parts of words.
* Vim method: Press three keys `c`hange `i`nside `"` (quotes), and start typing your replacement. This is desirable as it says what you actually wanted to do, behaves consistently and expectedly, and takes very few keypresses to achieve so you can be more productive overall.

Just like any workflow, Vim requires making small changes to learn. Like learning any other skill, you start out as a slow uncomfortable clumsy beginner, but with practice you can develop proficiency, speed, and more abilities.

The following pages discuss this well with details:

* [Learn Vim Progressively - Yann Esposito](https://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
* [How To Learn Vim: A Four Week Plan - Pete Jang](https://peterxjang.com/blog/how-to-learn-vim-a-four-week-plan.html)

You could also watch the Vimcasts from the beginning, and integrate these into your workflow:

* <http://vimcasts.org/episodes/archive/>

You can also run `vimtutor` on the commandline to start an interactive tutorial.

### Getting Help

If you are ever stuck, you can search the internet for the thing you want to do, with "vim" added.

Most likely you will find a Stack Overflow or [Vim Tips Wiki](https://vim.fandom.com/) page explaining how to do it.

If you don't know what a command, option, or setting within Vim does, get help with it using `:help thing` `:help :thing`

----

# todo

## vimrc

* keep it simple
* don't load many plugins

### Stop Using the Arrow Keys

### Plugins I Use

### Statusline

### Leader

## Favorite Tips and Tricks

### Modelines
