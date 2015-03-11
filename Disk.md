# Disk stuff
Operations for disk space, etc.

## File size

#### How to find total size on disk of certain filetypes, recursive.

In this case, total file size in GB of MP4 files by using combo of *find*, *du* and *awk*:

`find . -name "*.mp4" -print0 | du -sb --files0-from=-  | awk '{ total += $1} END { print total/1024/1024/1024 }'`

`find -name "*.mp4" -exec du -b {} \; | awk 'BEGIN{total=0}{total=total+$1}END{print total}'`

*"The -exec option of find command executes a simple command with {} as the file found by find. du -b displays the size of the file in bytes. The awk command initializes a variable at 0 and get the size of each file to display the total at the end of the command."*
