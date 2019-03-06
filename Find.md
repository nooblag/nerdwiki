# Find

### Find a file by filename

`find /path -iname "filename"`

`find /path -iname "*.wildcard" | less`

### Find a directory

``find /path -name DIRNAME -type d``

### Conditioning

Find files in the "travelphotos" directory that are greater than 200 kilobytes in size but do not have "2015" anywhere in the file name.

`find /travelphotos -type f -size +200k -not -iname "*2015*"`

`find . -size +500000 -print` - find any file above 500mb.

OR

`find . -size +500M -print` - same thing.

`find . -size +2G -print` - find any file above 2GB.

`for f in 'find . -size +5M'; do ls -la $f || break; done` - find any file above 5MB and run `ls -la` on it with a for loop.

Some more good explanatory info and exmaples [here](https://www.howtogeek.com/112674/how-to-find-files-and-folders-in-linux-using-the-command-line/).


### Find text inside a file
`grep -r 'text goes here' path_goes_here`

# Replace
Combo of `find` and `sed` to find and replace a string inside files, where *.ext* is type of files you're targeting, and *FOO* is replaced by *BAR*:

`find . -type f -name '*.ext' -exec sed -i 's|FOO|BAR|g' {} \;`

Could also use the `rpl` programme.
