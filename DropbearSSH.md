Dropbear is a lightweight SSH2 server. It uses a lot less resources than OpenSSH server.

`apt-get install dropbear`

### Config file is /etc/default/dropbear. In this file, modify the line -

`NO_START=1`

to read -

`NO_START=0`

This will enable dropbear to start up. Modify the line -

`DROPBEAR_EXTRA_ARGS=""`

to read -

`DROPBEAR_EXTRA_ARGS="-w"`

This will disable root logins.

### Next, disable OpenSSH from starting up at login -

`mv /etc/rc2.d/S16ssh /etc/rc2.d/K16ssh`

### Shutdown OpenSSH and start dropbear -

`/etc/init.d/ssh stop`

`/etc/init.d/dropbear start`

Test SSH is working, then restart the machine.
