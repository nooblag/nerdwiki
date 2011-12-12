### Setup Samba share to allow user to read/write to home directory

Edit `/etc/samba/smb.conf` and look for Authentication section and
change to this -

####### Authentication #######

# "security = user" is always a good idea. This will require a Unix
account
# in this server for every user accessing the server. See
# /usr/share/doc/samba-doc/htmldocs/Samba3-HOWTO/ServerType.html
# in the samba-doc package for details.

    security = user

    hosts allow =

    [share]
     comment = dudeshare
     path = /share/
     force user = samba
     force group = samba
     read only = No
     hosts allow =

Add a SMB password for an existing user -

`sudo smbpasswd -a nameofuser`

Then restart Samba with -

`sudo /etc/init.d/samba restart`

