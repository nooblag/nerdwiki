# Disk stuff
Operations for disk space, etc.

## File size

#### Show usage of all disks, human readable numbers
`df -h`

#### How to find total size on disk of certain filetypes, recursive.

In this case, total file size in GB of MP4 files by using combo of *find*, *du* and *awk*:

`find . -name "*.mp4" -print0 | du -sb --files0-from=-  | awk '{ total += $1} END { print total/1024/1024/1024 }'`

`find -name "*.mp4" -exec du -b {} \; | awk 'BEGIN{total=0}{total=total+$1}END{print total}'`

*"The -exec option of find command executes a simple command with {} as the file found by find. du -b displays the size of the file in bytes. The awk command initializes a variable at 0 and get the size of each file to display the total at the end of the command."*

## Swappiness

Set system to prefer swapping file data over application code (this does not matter if you have enough RAM to keep whole filesystem and all the application code and all virtual memory allocated by applications in RAM). This reduces latency for swapping between different applications over latency for accessing big files from a single application:

`echo 15 > /proc/sys/vm/swappiness`

*vfs_cache_pressure*
Controls the tendency of the kernel to reclaim the memory which is used for caching of directory and inode objects.

At the default value of vfs_cache_pressure=100 the kernel will attempt to reclaim dentries and inodes at a "fair" rate with respect to pagecache and swapcache reclaim. Decreasing vfs_cache_pressure causes the kernel to prefer to retain dentry and inode caches. When vfs_cache_pressure=0, the kernel will never reclaim dentries and inodes due to memory pressure and this can easily lead to out-of-memory conditions. Increasing vfs_cache_pressure beyond 100 causes the kernel to prefer to reclaim dentries and inodes.

https://unix.stackexchange.com/questions/30286/can-i-configure-my-linux-system-for-more-aggressive-file-system-caching
