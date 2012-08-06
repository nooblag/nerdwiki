## Basics

Print entire line - `awk '{print $0}'`

`$0` is the variable for the entire line.

`$1` is the first field before the next space. Each consecutive number (or variable) is the next field in the line.

### `$NF` variable

`$NF` is the number of fields variable. Can either print the number of fields in a line, or can manipulate the value to get to other fields based on it's position from the last field.

Example -

`echo 'this is just a test' | awk '{print $(NF-2), $1}'

will output `just this`
