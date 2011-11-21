## Turn screensaver off/on

`xset s on` (or off)

## Turn monitor off/on

`xset dpms force off` (or on)

## X over SSH

`echo $DISPLAY` should show :0.0

if not then set $DISPLAY var to allow X use over SSH.

### Set $DISPLAY in .bashrc file -

`DISPLAY=:0.0`

### Reload .bashrc with -

`source ~/.bashrc`
