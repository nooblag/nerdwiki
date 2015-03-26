# Find
## Example lines

`find . -size +500000 -print` - find any file above 500mb.

OR

`find . -size +500M -print` - same thing.

`find . -size +2G -print` - find any file above 2GB.

`for f in 'find . -size +5M'; do ls -la $f || break; done` - find any file above 5MB and run `ls -la` on it with a for loop.

# Replace
Combo of `find` and `sed` to find and replace a string inside files, where *.ext* is type of files you're targeting, and *FOO* is replaced by *BAR*:

`find . -type f -name '*.ext' -exec sed -i 's|FOO|BAR|g' {} \;`
