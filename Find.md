# Find

### Find a file by filename

`find /path -iname "filename"`

`find /path -iname "*.wildcard" | less`

Or

`find . -name index.php -type f`

If you want to search for files having names say findex.php, index.phpfoo, index.php you need to use:

`find . -name '*index.php*' -type f`

Where * is a glob pattern meaning zero or more characters.

On the other hand if you want to look in the current directory only :

`find . -maxdepth 1 -name '*index.php*' -type f`


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

#### Find files that haven't been modified for more than 2 minutes.

`find /path -mmin +2 -type f -print`

`find /path -maxdepth 1 -not -name ".htaccess" -not -name ".someotherfile" -mmin +2 -type f -print`

Using `maxdepth 1` means only in this folder, don't specify maxdepth to use full recursive. `-not -name` ignore certain files

Using `exec` at end instead of `-print` to do an action to matches, for example, to move matched files to another directory.

`find /path -maxdepth 1 -not -name ".htaccess" -mmin +2 -type f -exec mv {} /path/matches/ \;`

After `-exec` is the command to run. `{}` represents the file matched and `\;` concludes the command string.


### Find text inside a file

`grep -r 'text goes here' path_goes_here`

## Find available system commands
`compgen -c` will list all the commands you could run.

`compgen -c | sort` will show list in alphabetical order


# Replace
Combo of `find` and `sed` to find and replace a string inside files, where *.ext* is type of files you're targeting, and *FOO* is replaced by *BAR*:

`find . -type f -name '*.ext' -exec sed -i 's|FOO|BAR|g' {} \;`

Could also use the `rpl` programme.
