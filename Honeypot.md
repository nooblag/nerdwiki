## Installing Kippo honeypot

**Tested on Ubuntu 10.04 Server.**

`apt-get install python-twisted python-mysqldb subversion`

`adduser kippo`

`svn checkout http://kippo.googlecode.com/svn/trunk/ /home/kippo`

`cp /home/kippo/kippo.cfg.dist /home/kippo/kippo.cfg`

Login as kippo (won't run as root), start Kippo -

`./start.sh`

By default Kippo runs on port 2222. Run this command to route to default SSH 22 port (note: this command will have to be run again if system is restarted) -

`iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 22 -j REDIRECT --to-port 2222`

Log files are kept in `/home/kippo/log/tty`, downloaded files kept in `/home/kippo/dl`

## Configure kippo to log to MySQL (optional) -

`mysql -u root -p`

`create database kippo;`

`grant all privileges on kippo.* to 'kippo'@localhost identified by 'secret';`

`exit;`

`mysql -ukippo -psecret kippo < /home/kippo/doc/sql/mysql.sql`

Edit .cfg file to connect to MySQL database -

        [database_mysql] host = localhost
        databse = kippo
        username = kippo
        password = secret
