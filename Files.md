# chmod

To change all the directories to 755 (drwxr-xr-x):

`find /some/path -type d -exec chmod 755 {} \;`

To change all the files to 644 (-rw-r--r--):

`find /some/path -type f -exec chmod 644 {} \;`

# Bulk Rename files

`rename -v 's/FOO/BAR/' *.doc`

Where FOO is in .doc filenames, it's replaced with BAR.

Example:

`rename -v 's/\[//' *`

Replace bracket with blank space in any filenames. Bracket needs to be escaped.
