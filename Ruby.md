## Ruby on Rails install

Good setup for development.

Install RVM - 

`bash < <(curl -s https://rvm.beginrescueend.com/install/rvm)`

Add RVM to .bashrc file - 

`echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"' >> ~/.bashrc `

Install Ruby 1.9.2 - 

`rvm install 1.9.2`

Use 1.9.2 by default -

`rvm use 1.9.2 --default`

## Cool Ruby gems

* cheat
* gollum
* rails
* jekyll

## Errors and workarounds

zlib not installed

`rvm pkg install zlib`

`rvm remove 1.9.1`

`rvm install 1.9.1 -C --with-zlib-dir=$rvm_path/usr`
