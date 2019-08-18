### Grab text files only
Brackets iterate, to capture extensions both in caps or lowercase

`rsync -vahP --include="*/" --include="*.[Tt][Xx][Tt]" --exclude="*" /from/ /to/`


#### Only upload MP4s:
`rsync -vahP --preallocate --include="*/" --include="*.mp4" --exclude="*" /from/ /to/`

### Ignore groups, permissions:
`rsync -vahP --no-perms --no-owner --no-group --stats`

### Exclude hidden folders, but Include specific ones
`rsync -vahPn --delete-before --include={'.ssh/','.bash_history'} --exclude={'.*/','.*'} ./ /mount/anotherdisk/username/`
