# chmod

To change all the directories to 755 (drwxr-xr-x):

`find /some/path -type d -exec chmod 755 {} \;`

To change all the files to 644 (-rw-r--r--):

`find /some/path -type f -exec chmod 644 {} \;`
