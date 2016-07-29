## Example usages

__Note__ that `sed` does not write to a file, only echos the result. Pipe to another file to save result.

### Find and print

`sed -n '/thingtofind/p'`

### Find a word and replace it

`sed -e 's/wordtoreplace/replacementword/g' filename.txt`
