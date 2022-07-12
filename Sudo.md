# How to Add a User to the Sudoers List

`sudo usermod -aG sudo usernamehere`

`-a` is for the Append operation, and `-G` specifies the sudo Group.

# Modify user's sudo permissions

`sudo visudo`

this opens `/etc/sudoers` file

Make sure the following line is uncommented in the file.

`%wheel  ALL=(ALL)       ALL`

By default, even if a user is part of wheel group, you need to provide the password every time you run a command as sudo. If you need passwordless sudo access, you need uncomment the following where it has NOPASSWD and save the file

`%wheel  ALL=(ALL)       NOPASSWD: ALL`

## Adding sudo privileges for specific commands

You might want only specific commands to be run a sudo privileges for a specific user... You can group the set of commands to be run under `Cmnd_Alias`

For example, if you open the `/etc/sudoers` file, you may find the following aliases:

```
## Networking
# Cmnd_Alias NETWORKING = /sbin/route, /sbin/ifconfig, /bin/ping, /sbin/dhclient, /usr/bin/net, /sbin/iptables, /usr/bin/rfcomm, /usr/bin/wvdial, /sbin/iwconfig, /sbin/mii-tool

## Installation and management of software
# Cmnd_Alias SOFTWARE = /bin/rpm, /usr/bin/up2date, /usr/bin/yum

## Services
Cmnd_Alias SERVICES = /sbin/service, /sbin/chkconfig, /usr/bin/systemctl start, /usr/bin/systemctl stop, /usr/bin/systemctl reload, /usr/bin/systemctl restart, /usr/bin/systemctl status, /usr/bin/systemctl enable, /usr/bin/systemctl disable
```

If you want a user to have only permissions to run commands under the SERVICES alias, you need to have the following entry in the `/etc/sudoers` file

`username            ALL = SERVICES`


Another example:

`sudo visudo`

Specify specific commands that can be invoked without password:

```
# Allow specific users to apply software updates without password
username  ALL=(ALL) NOPASSWD:/usr/bin/apt update, /usr/bin/apt full-upgrade, /usr/bin/apt autoremove
```
