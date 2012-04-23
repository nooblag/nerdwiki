### Create an image of a partition and skip bad blocks and errors

`sudo dd bs=512 if=/dev/disk0s3 of=/Volumes/Backup/backup.dmg conv=noerror,sync`

### Testdisk

Use this, it's really good for recovering partitions that have been erased.

## Destroying data

### Zero out a hard drive

`dd if=/dev/zero of=/dev/pathtodevice`

Only one pass is needed.

## dcfldd

Improved version of `dd`. Includes progress bar, among other things.

## iPhone

### Backup a jailbroken iPhone -

`ssh root@jphone dd if=/dev/rdisk0 bs=1M | dd of=iphonebak.img`
