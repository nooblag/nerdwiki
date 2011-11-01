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
