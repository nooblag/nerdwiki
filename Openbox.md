Start with `openbox-session`. This starts openbox as a bare window manager.

After making changes to config and menu files, run `openbox --reconfigure`

### Config files

`~/.config/openbox/rc.xml` - cp from default config `/etc/xdg/openbox/rc.xml` and edit to your liking.

### Menus

`aptitude install obmenu` - GUI menu editor, easiest way to get started.

User default menu file located at `~/.config/openbox/menu.xml`

### Desktop background

Use `feh` to set background in your `autostart.sh` script -

`feh --bg-scale "$HOME"/path/to/wallpaper.jpg &`

The `&` runs `feh` as a background process.

## Errors and workarounds

If your `~/.config/openbox/autostart.sh` script isn't loading on start, make sure you are starting openbox using `openbox-session` rather than `openbox`, as the later won't load your `autostart.sh` script, and also make sure the script is executable (`chmod +x ~/.config/openbox/autostart.sh`).
