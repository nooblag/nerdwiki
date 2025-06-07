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

### Take Two

https://stackoverflow.com/a/8417536

`for i in *-doc-*.txt; do mv "$i" "${i/*-doc-/doc-}"; done`

Where `${i/*-doc-/doc-}` replaces the first occurrence of `*-doc-` with `doc-`


### A bash example

Rename to clean up something `SOV.0123.4567.8910 Crap with spaces.pdf` to `SOV.0123.4567.8910.pdf`

```
for i in *; do
  mv "${i}" "$(echo "${i}" | sed 's/\(SOV\.[[:digit:]]\{4\}\.[[:digit:]]\{4\}\.[[:digit:]]\{4\}\).*\(\..*\)/\1\2/g')"
done
```



# Display contents of a file ignoring comments

`grep -v '^;' /etc/php/8.0/fpm/php.ini | grep -v '^$'`

If needing '#' for comments, change `grep -v '^;'` to `grep -v '^#'`

Pipe to `grep -v '^$'` removes blank lines


# chattr

Make file immutable/undeletable. This implies that the file can’t be modified in any way: it can’t be deleted or renamed. You can’t even create a link to it and no data can be written to the file as well.

`sudo chattr +i FILE`

Make it normal again

`sudo chattr -i FILE`

View attributes of existing:

`lsattr FILE`

Can do it recursive on a folder also:

`sudo chattr +i -RV path/`

