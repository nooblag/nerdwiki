## Split a large file (8gb) into 2gb chunks

`split -b 2048m filetosplit.tar`

This will split the file into smaller files with filenames `xaa`, `xab`, `xac` and so on. To join files together again, use `cat`. E.g. -

`cat xa* >> filetosplit.tar`
