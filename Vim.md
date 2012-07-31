## Navigating

* nG - jump to line n ("line 5, Go")
* C-o - jump backwards ("out")
* C-i - jump forwards ("in")
* L - jump to bottom of screen ("low")
* M - jump to middle of screen ("middle")
* H - jump to top of screen ("high")
* zt - put this line at the 't'op of the screen
* zb - put this line at the 'b'ottom of the screen
* zz - put this line at the middle of the screen

* . - in command mode, this will repeat last command

## Deleting

Delete lines with a pattern -

`:g/whattodelete/d`

## Installing

On Debian. From source, with ruby & python syntax support.

Download vim - `curl -O ftp://ftp.vim.org/pub/vim/unix/vim-7.3.tar.bz2` and untar.

Install ncurses, lua & ctags dependencies - `aptitude install libncurses5-dev lua5.2 ctags`

Configure - `./configure --with-features=huge --enable-luainterp \\n            --enable-perlinterp --enable-pythoninterp \\n            --enable-rubyinterp --enable-gui=gtk2 \\n            --disable-largefile`

Then `make && sudo make install`
