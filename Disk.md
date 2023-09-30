# Disk stuff
Operations for disk space, etc.

## Disk Speed

#### Test disk write speed

Write 2,048 counts of 512k to test writing a 1GB file:

`dd if=/dev/zero of=/tmp/speedtest.garbage bs=512k count=2048 oflag=direct`

An average SSD speed is around 150MB/s.

One-liner that writes a 4GB test, show progress, and cleans-up:

`temp="$(mktemp)" && dd if=/dev/zero of="${temp}" bs=1024k count=4096 oflag=direct status=progress; rm "${temp}"`


## File size

#### Show usage of all disks, human readable numbers
`df -h`

#### To list the top 10 largest files from the current directory
`du -h . | sort -nr | head -n10`

#### To list the largest directories from the current directory
`du -sh * | sort -nr | head -n10`


#### How to find total size on disk of certain filetypes, recursive.

In this case, total file size in GB of MP4 files by using combo of *find*, *du* and *awk*:

`find . -name "*.mp4" -print0 | du -sb --files0-from=-  | awk '{ total += $1} END { print total/1024/1024/1024 }'`

`find -name "*.mp4" -exec du -b {} \; | awk 'BEGIN{total=0}{total=total+$1}END{print total}'`

*"The -exec option of find command executes a simple command with {} as the file found by find. du -b displays the size of the file in bytes. The awk command initializes a variable at 0 and get the size of each file to display the total at the end of the command."*

## Swappiness

`echo 100 > /proc/sys/vm/swappiness`

If you prefer to keep applications nearly always in RAM you could set this to 1. If you set this to zero, kernel will not swap at all unless absolutely necessary to avoid Out Of Memory. If you were memory limited and working with big files (e.g. HD video editing), then it might make sense to set this close to 100.

By setting swappiness high (like 100), the kernel moves everything it doesn't need to swap, freeing RAM for caching files.

*vfs_cache_pressure*

`echo 1 > /proc/sys/vm/vfs_cache_pressure`

Setting *vfs_cache_pressure* to low value makes sense because in most cases, the kernel needs to know the directory structure before it can use file contents from the cache and flushing the directory cache too soon will make the file cache next to worthless. Consider going all the way down to 1 with this setting if you have lots of small files (my system has around 150K 10 megapixel photos and counts as "lots of small files" system). Never set it to zero or directory structure is always kept in memory even if the system is running out of the memory. Setting this to big value is sensible only if you have only a few big files that are constantly being re-read (again, HD video editing without enough RAM would be an example case). Official kernel documentation says that "increasing vfs_cache_pressure significantly beyond 100 may have negative performance impact".

At the default value of vfs_cache_pressure=100 the kernel will attempt to reclaim dentries and inodes at a "fair" rate with respect to pagecache and swapcache reclaim. Decreasing vfs_cache_pressure causes the kernel to prefer to retain dentry and inode caches. When vfs_cache_pressure=0, the kernel will never reclaim dentries and inodes due to memory pressure and this can easily lead to out-of-memory conditions. Increasing vfs_cache_pressure beyond 100 causes the kernel to prefer to reclaim dentries and inodes.

By setting vfs_cache_pressure lower (maybe 1), it will favor caching files instead of keeping application data in RAM.

To change the system swappiness value, open `/etc/sysctl.conf` as root. Then, change or add this line to the file:

`vm.swappiness = 10`

Reboot for the change to take effect.

You can change the value while your system is still running with:

`sysctl vm.swappiness=10`


https://unix.stackexchange.com/questions/30286/can-i-configure-my-linux-system-for-more-aggressive-file-system-caching

https://www.kernel.org/doc/Documentation/sysctl/vm.txt

https://askubuntu.com/questions/103915/how-do-i-configure-swappiness

## Handy disk cache tool?

`vmtouch` - the Virtual Memory Toucher.

Portable file system cache diagnostics and control

https://hoytech.com/vmtouch/

https://github.com/hoytech/vmtouch
