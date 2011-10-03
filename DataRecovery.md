## Create an image of a partition and skip bad blocks and errors

`sudo dd bs=512 if=/dev/disk0s3 of=/Volumes/Backup/backup.dmg conv=noerror,sync`

This is essentially what data recovery specialists do anyway. But heaps cheaper.

## Testdisk

Use this, it's really good for recovering partitions that have been erased.

## Helen's boot CD

Was that what I used to recover Nugg's failing Windows HD? I think so. It's a live CD, grab that.
