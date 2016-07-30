## Install

### Debian

Tested on [version 8.3](https://www.debian.org/News/2016/20160123); based on [these instructions](http://pkg.jenkins-ci.org/debian/), and also [these ones](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).

1. `wget -q -O - http://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -`
2. `echo "deb http://pkg.jenkins.io/debian binary/" >> sources.list`
3. `sudo apt-get update && sudo apt-get install jenkins`
4. Jenkins will fail to start; to fix edit `/etc/default/jenkins` and change `HTTP_PORT=8080` to `HTTP_PORT=8081`
5. `sudo service jenkins restart`
