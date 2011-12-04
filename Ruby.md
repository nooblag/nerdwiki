## Ruby on Rails install

Good setup for development.

#### Install RVM - 

`bash < <(curl -s https://rvm.beginrescueend.com/install/rvm)`

#### Add RVM to .bashrc file - 

`echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"' >> ~/.bashrc`

#### Install Ruby 1.9.2 - 

`rvm install 1.9.2`

#### Use 1.9.2 by default -

`rvm use 1.9.2 --default`

## Cool Ruby gems

* cheat - cheat sheets for all sorts of misc stuff
* gollum - git based wiki
* rails - ruby on rails
* jekyll - static blog generator

## Errors and workarounds

### zlib not installed

`rvm pkg install zlib`

`rvm remove 1.9.2`

`rvm install 1.9.2 -C --with-zlib-dir=$rvm_path/usr`
