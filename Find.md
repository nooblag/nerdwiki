## Example usages

### Find any file above 500MB

`find . -size +500M -print`

### Find any file above 2GB

`find . -size +2G -print`

### Find any file above 5MB and loop over results

`for f in `find . -size +5M`; do ls -la $f || break; done`
