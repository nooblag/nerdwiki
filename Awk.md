## Basics

Print entire line - `awk '{print $0}'`

`$0` is the variable for the entire line.

`$1` is the first field before the next space. Each consecutive number (or variable) is the next field in the line.

`awk` uses whitespace as a delimiter to seperate fields.

### `$NF` variable

`$NF` is the number of fields variable. Can either print the number of fields in a line, or can manipulate the value to get to other fields based on it's position from the last field.

Example -

`echo 'this is just a test' | awk '{print $(NF-2), $1}'`

will output `just this`

## Example usages

### Show accepted SSH connections from log

`sudo grep -w 'sshd' /var/log/auth.log | grep -w 'Accepted' | awk '{ print "User: "$9 " Time: "$1 " "$2 " "$3 }'`

### Use colon (:) instead of whitespace as delimiter

`awk -F ':' '{ print $1 $2 }' file.txt`

### Print directory names and sizes and format nicely

`du -hd 1 | sort -nr | awk -F './' '{ print "Folder: "$2" \nSize: "$1 }'`
