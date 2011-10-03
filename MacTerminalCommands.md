## Fix home permissions

`sudo chmod -R ug+rwX /Users/username`

## List and sort files by filesize

Useful for finding what files are taking up the most space.

`du -h | sort -nr`

## List open ports and the processes using them

`lsof -i`

`lsof -i tcp:8254`

## List all loaded third-party kernel extensions

`kextstat | grep -v com.apple`

## List files that running applications/processes are accessing

Find application/process with `ps aux`

`ps aux | grep nameofapp`

Then use opensnoop with name of application or process ID.

`sudo opensnoop -n [nameofapp]`

`sudo opensnoop -p 2837`

## Show hidden files in Finder

Use FALSE to hide files again.

`defaults write com.apple.Finder AppleShowAllFiles TRUE`

## List history of reboots and shutdowns

`last reboot`

`last shutdown`

Use grep to find reboots or shutdowns in a certain month.

`last reboot | grep May`

## Eject and close DVD drive

`drutil tray eject`

`drutil tray close`

## 10.7 Lion

Change password of current user with no prompt for old password

`dscl localhost -passwd /Search/Users/Josh`

## Misc.

`launchctl load /Library/LaunchDaemons/`

`lsbom .pkg/Contents/Archive.bom> | more`

`sudo defaults write /Library/Preferences/com.apple.iWork09.Installer InstallMode -string 'Retail'`
