Installing Ubuntu 10.10 and removing all the crap

### Desktop

Uninstall Evolution and clean up it's mess -- manually del indicator-messages and other junk:
`sudo apt-get remove evolution-indicator`
`sudo apt-get remove indicator-messages`
`sudo apt-get remove indicator-me`
`killall gnome-panel`

