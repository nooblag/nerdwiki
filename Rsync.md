#### A nice backup line

`rsync -avzR --dry-run --exclude=home/YOU/{Media/Movies,Media/Music,Downloads,Backups,.local/share/Trash,.thumbnails,.cache,.mozilla/firefox/*.default/Cache,.mozilla/firefox/*.default/OfflineCache,.gvfs} /home/YOU /mnt/external/drive/place`

#### Only upload MP4s
`rsync -varhPz --preallocate --include="*/" --include="*.mp4" --exclude="*" "/media/User/dir/to/cdn/" root@SERVERIP:/var/www/html/`
