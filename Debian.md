## Debian Web & Mail Server

Only 100mb RAM usage with the following running. Very fast and quick web server.

Installed -

* nginx
* dropbear
* postgreSQL
* mediawiki
* postfix
* dovecot
* fail2ban

OpenSSH, apache2, mysql turned off or uninstalled.

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

* Edit hostfile
* Disable IPv6
* Install NVidia
* Install smbfs
* Change keyboard layout to Macintosh 
