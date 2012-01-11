## Home setup

Debian squeeze 6, 64-bit CD iso.

Only install OpenSSH server and essential system utilities.

## Steps once installed and rebooted into new system -

`aptitude install git git-core` and clone dotfiles.

`aptitude install screen`

`apt-get install --no-install-recommends xorg xfce4 alsa-base alsa-utils cpufrequtils gamin xdg-utils desktop-base gnome-brave-icon-theme dmz-cursor-theme`

`aptitude install terminator dolphin iceweasel rhythmbox`

Comment out CD-ROM from apt sources list, and add Multimedia repo -

`nano /etc/apt/sources.list`

Add `deb http://www.debian-multimedia.org stable main non-free`

Install screensavers -

`aptitude install xscreensaver-gl xscreensaver-gl-extra xscreensaver`

* Edit hostfile
* Disable IPv6
* Install NVidia
* Install smbfs
* Change keyboard layout to Macintosh 

## Install PHP on Debian without Apache

Installing `php5-cgi` package before installing `php5` package allows you to install PHP5 without installing Apache. `php5-cgi` package satisfies the dependencies that Apache provides.

## HFS read/write

Need to disable journaling in MacOS on the target drive.

`sudo aptitude install hfsplus hfsutils hfsprogs`

Edit `/etc/fstab` -

`defaults,force,rw`

Make sure all userfiles have uid of 501 -

`find / -uid 1000  -exec chmod 501 "{}" \`

## Firefox

Install Firefox -

Download latest 64bit from https://ftp.mozilla.org/pub/mozilla.org/firefox/nightly/latest-trunk/

Untar, create a symbolic link to `firefox` in the extracted folder to `/usr/bin/firefox`
