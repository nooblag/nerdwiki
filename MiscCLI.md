### List processes with open ports -

`sudo netstat -tpl`

### Tar

Compress a file -

`tar -czvf whatever.tar foldername`

Untar a file -

`tar -xvf whatever.tar`

### Change timezone -

`sudo dpkg-reconfigure tzdata`

### Navigating directories

Move to another directory but keep current directory in memory so you can navigate back easily -

`pushd ~` (or whatever directory)

To go back to directory you 'pushd' -

`popd`

### Find a file

Search in home directories -

`find /home -name 'hello.c'`

### Play a random episode of Seinfeld in VLC fullscreen

`find /mnt/media -name "Seinfeld*.avi" | sort -R | head -n1 | xargs -d '\n' vlc -f`

### Play sound like you're on the Starship Enterprise

`play -n -c1 synth whitenoise band -n 100 20 band -n 50 20 gain +25 fade h 1 864000 1`

### List most used commands from history

`history | cut -c8- | sort | uniq -c | sort -rn | head`

### Run a command every 2 seconds

`watch -n2 "ps aux|grep ssh"`

### Rename files in shell

Change all files with `.SMS` extension to lowercase `.sms` extension -

`rename 's/\.SMS/.sms/' *.SMS`

### Split a large file (8gb) into 2gb chunks

`split -b 2048m filetosplit.tar`

This will split the file into smaller files with filenames `xaa`, `xab`, `xac` and so on. To join files together again, use `cat`. E.g. -

`cat xa* >> filetosplit.tar`

### Print size of directories

`du -hd 1`
