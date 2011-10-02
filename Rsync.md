A nice backup line -

`rsync -avzR --dry-run --exclude=home/YOU/{Media/Movies,Media/Music,Downloads,Backups,.local/share/Trash,.thumbnails,.cache,.mozilla/firefox/*.default/Cache,.mozilla/firefox/*.default/OfflineCache,.gvfs} /home/YOU /mnt/external/drive/place`
