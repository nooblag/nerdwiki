## Example lines

`find . -size +500000 -print` - find any file above 500mb.

OR

`find . -size +500M -print` - same thing.

`find . -size +2G -print` - find any file above 2GB.

`for f in `find . -size +5M`; do ls -la $f || break; done` - find any file above 5MB and run `ls -la` on it with a for loop.
