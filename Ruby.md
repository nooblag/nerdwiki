### Ruby on Rails install

Good setup for development.

Install RVM - 

`bash < <(curl -s https://rvm.beginrescueend.com/install/rvm)`

Add RVM to .bashrc file - 

`echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"' >> ~/.bashrc`

Install Ruby 1.9.2 - 

Note: installing zlib now will help save compatability woes with certain gems later on.

`rvm pkg install zlib`

`rvm install 1.9.2 -C --with-zlib-dir=$rvm_path/usr`

Use 1.9.2 by default -

`rvm use 1.9.2 --default`

### Cool Ruby gems

* cheat - cheat sheets for all sorts of misc stuff
* gollum - git based wiki
* rails - ruby on rails
* jekyll - static blog generator

### Start a new Sinatra application

Stolen from [Learn Ruby the Hard Way.](http://ruby.learncodethehardway.org/book/ex50.html)

`gem install sinatra`

Start new project folder/repo -

`bundle gem nameofproj`

Edit `lib/nameofproj.rb` to contain -

  require_relative "nameofproj/version"
  require "sinatra"

  module nameofproj
    get '/' do
      greeting = "Hello, World!"
      return greeting
    end
  end

Then start the application with -

`ruby lib/nameofproj.rb`

