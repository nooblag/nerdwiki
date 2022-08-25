Note that sed does not write to a file, only echos the result. Use `-i` "in place" to save the find/replace result to the file.

### Find and print

`sed -n '/thingtofind/p'`

### Find a word and replace it

`sed -e 's/wordtoreplace/replacementword/g' filename.txt`
