## Anonymous browsing

Adds a new user account and opens firefox as that user.

`useradd -m anonymous`

`sudo -H -u anonymous firefox`

## Assign apps to protocols

Type `about:config` into the address bar.

Add a new boolean preference named `network.protocol-handler.expose.rtsp`, set to `false`

Firefox will now ask what app you would like to use when opening an `rtsp` link.
