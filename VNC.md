## Autostart VNC server

Tested on Debian Wheezy.

Ensure `x11vnc` is installed with `aptitude install x11vnc`

Add the following line to `~/.xsessionrc` -

`x11vnc -display :0 -bg -nopw -noxdamage -forever`
