# Basic cheatsheet for Vim


Notes taken from: https://www.linux.com/tutorials/vim-101-beginners-guide-vim/

## Opening vim


Open/create file with the command:

```
vim <filename>

```
Vim will open in `command` mode. This means when you enter `j` the character won't be entered, instead this will issue the command to move the cursor down one line.


## Insert mode

To type normally, enter the `insert` mode by typing `i`.

To exit the `insert` mode type `esc`.

## Moving around document

In `command` mode the following commands navigate through a file:

* `h` moves the cursor one character to the left.
* `j` moves the cursor down one line.
* `k` moves the cursor up one line.
* `l` moves the cursor one character to the right.
* `0` moves the cursor to the beginning of the line.
* `$` moves the cursor to the end of the line.
* `w` move forward one word.
* `b` move backward one word.
* `G` move to the end of the file.
* `gg` move to the beginning of the file.
* `backtick.` move to the last edit.

*Handy tip: prefacing a movement command with a number will execute that movement multiple times. So, if you want to move up six lines, enter 6k and Vim will move the cursor up six lines. If you want to move over five words, enter 5w. To move 10 words back, use 10b.*


## Editing the document

In command mode:


* `x` deletes the character cursor is on
* `u` undo previous command
* `ctrl-r` undo the undo!
* `dw` delete word from the cursor to end of word
* `db` delete word from cursor to start of word
* `d0` delete to beginning of the line
* `d$` delete to end of the line
* `dgg` delete to beginning of the file
* `dG` delete end of the file


## Search and replace

To search for a term, in the `command` mode `/search-term`. To move to the next instance of the search term, enter `n` to move to the previous instance, enter `N`. 

Using `/search-term` will search from the current position, down the document. Using `?search-term` will search from the current position up the document. 

To search and then replace text:
```
:%s/text/replacement text/g
```
Will search through the document and replace `text` with `replacement text`. If you want to confirm each instance of the replacement:
```

:%s/text/replacement text/gc
```
## Copy and pasting


Text that's been deleted is saved to the clipboard so you can paste text that's been deleted. 

To select text, in the command mode select `v` then the standard movement keys `h, j, k , l` or to select lines, enter `ctrl-v`.

To copy the selected text, enter `y` to "yank" the text into the clipboard, to paste, use `p`.


Summary:

* `v` highlight one character at a time.
* `V` highlight one line at a time.
* `Ctrl-v` highlight by columns.
* `p` paste text after the current line.
* `P` paste text on the current line.
* `y` yank text into the copy buffer

## Save and quit

In the command mode, enter `:` and you’ll see a line at the bottom of the screen with a cursor ready to take input.

To write the file you’re editing, enter w. (So, you’ll have :w.) That will write the file to the existing filename. If you don’t have a filename or want to write out to a different filename, use :w filename.

To quit Vim after you’ve finished, hit :q. Since Vim is your friend, it won’t just pop out on you if you haven’t saved your file. It will say “no write since last change,” and suggest that you add ! to override.


## Adding plugins

First create the required directory and config file.

```
mkdir ~/.vim
vim ~/.vimrc
```

I used the `Vundle` package manager: https://github.com/VundleVim/Vundle.vim. Follow the instructions to install. Once you've listed your plugins in `.vimrc`, saved the file then in the `command/normal` mode type `:PluginInstall` to install the plugins. Restart the shell to see changes. 



## Copy and paste from Windows into vim

Need to check if clipboard support is available:

From the console, type:

```
vim --version | grep clipboard
```

If you see +clipboard or +xterm_clipboard, you are good to go. If it's `-clipboard` and `-xterm_clipboard`, you will need to look for a version of Vim that was compiled with clipboard support. On Debian and Ubuntu, to obtain clipboard support install the packages `vim-gtk` or `vim-gnome` (not `vim-tiny`).

Also, the following should work:
* `shift + del` to cut
* `ctrl + insert` to copy
* `shift + insert` to paste 

## Spell check

```
:set spell
:set nospell
```


