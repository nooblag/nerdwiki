### Setup Samba share to allow user to read/write to home directory

Edit `/etc/samba/smb.conf` and look for Authentication section and
change to this -

    ####### Authentication #######
    
    # "security = user" is always a good idea. This will require a Unix account
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

Next, find the Share Definitions section and change to allow users to
write to their home directories - 

    # By default, the home directories are exported read-only. Change the
    # next parameter to 'no' if you want to be able to write to them.
       read only = no

Add a SMB password for an existing user -

`sudo smbpasswd -a nameofuser`

Then restart Samba with -

`sudo /etc/init.d/samba restart`

### Add a share

Edit `/etc/samba/smb.conf` under Share Definitions section -

    [sharename]
    path = /path/to/share
    write list = nameofuser

Restart Samba with `sudo /etc/init.d/samba restart` after editing.

