# pi

## 720p video

Using Raspbian.

Edit `/boot/config.txt` to add -

`gpu_mem=64`

Start playing video from CLI with -

`omxplayer -o hdmi nameoffile.mkv`
