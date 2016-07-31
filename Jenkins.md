## Install

### Debian

Tested on [version 8.3](https://www.debian.org/News/2016/20160123); based on [these instructions](http://pkg.jenkins-ci.org/debian/), and also [these ones](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).

1. `wget -q -O - http://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -`
2. `echo "deb http://pkg.jenkins.io/debian binary/" >> sources.list`
3. `sudo apt-get update && sudo apt-get install jenkins`
4. Jenkins will fail to start; to fix edit `/etc/default/jenkins` and change `HTTP_PORT=8080` to `HTTP_PORT=8081`
5. `sudo service jenkins restart`

#### Install Node.js

__NOTE__: using [Vagrant](https://www.vagrantup.com/).

1. Install [`nvm`](https://github.com/creationix/nvm): `wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.4/install.sh | bash`
2. Install [Node.js](http://nodejs.org/) version `4.4.7`: `nvm install 4.4.7`
3. Set default Node.js version: `nvm use 4.4.7 --default`
4. In Jenkins, use full path to `npm`: `/home/vagrant/.nvm/versions/node/v4.4.7/bin/npm`

#### Install MySQL

__NOTE__: using [Vagrant](https://www.vagrantup.com/).

1. Edit `/etc/apt/sources.list`:
        deb http://packages.dotdeb.org jessie all
        deb-src http://packages.dotdeb.org jessie all
2. Add [Dotdeb](https://www.dotdeb.org/instructions/) repo keys: `wget https://www.dotdeb.org/dotdeb.gpg && sudo apt-key add dotdeb.gpg`
3. Update sources: `sudo apt-get update`
4. Install [MySQL](https://www.mysql.com/): `sudo apt-get install mysql-server`
