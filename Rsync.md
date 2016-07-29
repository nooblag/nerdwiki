### Example usages

#### Copy only certain files

`rsync -avPh {'file1.txt','file2.txt'} /target/directory`

#### Thorough backup

`rsync -avzR --dry-run --exclude=home/YOU/{Media/Movies,Media/Music,Downloads,Backups,.local/share/Trash,.thumbnails,.cache,.mozilla/firefox/*.default/Cache,.mozilla/firefox/*.default/OfflineCache,.gvfs} /home/YOU /mnt/external/drive/place`

#### DigitalOcean droplet restore

`rsync -aAXvzh --dry-run -e "ssh -p PORT" --exclude={/dev,/proc,/sys,/tmp,/run,/mnt,/media,/lost+found,sysconfig/} user@server:/ /path/to/backup/folder/`

Using `-aAX` as we then transfer in archive mode ensuring that symbolic links, devices, permissions and ownerships, modification times, ACLs and extended attributes are preserved. `-vzh` for verbose and compress and human progress.

### Resources

- https://wiki.archlinux.org/index.php/Full_system_backup_with_rsync
