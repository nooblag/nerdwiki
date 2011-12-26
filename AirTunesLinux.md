Tested on Debian Squeeze

### Install dependencies

`sudo aptitude install libcrypt-openssl-rsa-perl libao-dev`

`sudo aptitude install libaio1 libio-socket-inet6-perl avahi-dnsconfd  avahi-utils avahi-discover avahi-daemon openssl build-essential libsigc++-2.0-dev pkg-config comerr-dev libcurl4-openssl-dev libidn11-dev libkrb5-dev libssl-dev zlib1g-dev libncurses5 libncurses5-dev`

### Download Shairport

Version 0.05 used at time of writing.

`cd` to Shairport directory and run `make`. Copy `shairport.pl` and `hairtunes` to home directory.

Start with `perl shairport.pl`

