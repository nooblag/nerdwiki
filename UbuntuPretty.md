Installing Ubuntu 10.10 and removing all the crap

## Desktop

Uninstall Evolution and clean up it's mess -- manually del indicator-messages and other junk:

`sudo apt-get remove evolution-indicator`

`sudo apt-get remove indicator-messages`

`sudo apt-get remove indicator-me`

`killall gnome-panel`


## Boot

Modify Grub menu (dodgy), disable boot splash screen, and set login to text:

Run `sudo gedit /etc/default/grub` and change `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"` to `"text"`
After this run `sudo update-grub2`


## Add progras

`sudo apt-get install irssi`
