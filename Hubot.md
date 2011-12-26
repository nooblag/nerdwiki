### Installing npm and node.js

Install npm with `curl http://npmjs.org/install.sh | sudo sh`

Install redis-server package with `sudo aptitude install redis-server`

Install NVM for easy node.js version management -

`git clone git://github.com/creationix/nvm.git ~/.nvm`

Add `. ~/.nvm/nvm.sh` to ~/.bashrc or equivalent to activate nvm.

Install node.js version 0.6.5 with `nvm install v0.6.5`. Use `nvm use v0.6.5` to activate.

### Create a new bot

`git clone git://github.com/github/hubot.git`

`cd hubot`

`npm install`

`bin/hubot --create ~/bigbrobot`

Then `cd` to `~/bigbrobot` or whatever path you entered to work on the bot.

### Use with IRC

More configuration info and options @ https://github.com/github/hubot/wiki/Adapter:-IRC

Edit `package.json` file and add the following to dependencies area -

`"hubot-irc": "0.0.6"`

Run `npm install` to install dependencies.

Configure bash variables for bot -

`export HUBOT_IRC_SERVER="irc.server.org"`

`export HUBOT_IRC_ROOMS="#room,#chat"`

Start with `bin/hubot -a irc --enable-slash --name botname`

### Errors and workarounds

Node-expat error; Libexpat header files are missing -

`sudo aptitude install libexpat-dev`

Redis connect error; redis-server package is missing -

`sudo aptitude install redis-server`

