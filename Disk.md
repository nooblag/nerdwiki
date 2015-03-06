# Disk stuff
Operations for disk space, etc.

## File size

#### How to find total size on disk of certain filetypes, recursive.

In this case, total file size in GB of MP4 files by using combo of *find*, *du* and *awk*:

`find . -name "*.mp4" -print0 | du -sb --files0-from=-  | awk '{ total += $1} END { print total/1024/1024/1024 }'`
