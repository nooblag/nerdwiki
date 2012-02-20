### Mount samba network share

`sudo mount -t smbfs -o username=user,password=pass //192.168.0.20/Media /mnt/media`

### Mount drives with UUID and /etc/fstab

`sudo blkid` to get UUID of partition

`sudo nano /etc/fstab`

Example of mounting a FAT partition to allow user read/write -

`UUID=819B-F1D3 /mnt/files vfat user,rw,uid=1000,gid=100 0 0`

### Mount ext3 partition with read/write for user in /etc/fstab

`UUID=819B-F1D3 /mnt/files ext3 defaults,rw 0 0`

Note - may need to chown /mnt/files to allow user read/write.

### Add a samba share to /etc/fstab

`//192.168.0.20/Media /mnt/media smbfs user,rw,uid=1000,gid=100,username=user,password=pass 0 0`

Use `umask=100` for just read/write for all instead of UID.

If a space is needed in the share name, use octal \040, eg `//192.168.0.20/TV\040Shows`

### Mount an .ISO image

`sudo mkdir /tmp/cdrom`

`sudo mount -o loop,exec path_to_.iso /tmp/cdrom`

### Misc.

Refresh fstab with `mount -a`, unmount all with `umount -a`
