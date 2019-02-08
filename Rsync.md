#### Only upload MP4s
`rsync -varhPz --preallocate --include="*/" --include="*.mp4" --exclude="*" "/media/User/dir/to/cdn/" root@SERVERIP:/var/www/html/`

#### Ignore groups, permissions, 
`rsync -vahP --no-perms --no-owner --no-group --stats`
