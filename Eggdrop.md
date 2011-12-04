## Set up a Talking Eggdrop IRC Bot

TODO:

* Eggdrop tcl files and scripts and stuff.
* alice.tcl and egghttp.tcl
* pandorabots.com
* Running bot after setup without -m, add startup script to init.d

---

Using Ubuntu 10.04, but also tested on 9.10.

### Install eggdrop using apt -

`sudo apt-get install eggdrop`

### Edit config file and add the following lines near the end of the file -

`source scripts/egghttp.tcl`

`source scripts/alice.tcl`

### Setup new user just for eggdrop -

`sudo useradd -c “eggdrop” -m -s “/bin/bash” eggdrop`

### Set a password for the new user -

`sudo passwd eggdrop`

### Add symbolic links for the eggdrop scripts and modules folders to the new user’s home folder -

`ln -s /usr/lib/eggdrop/modules /home/eggdrop/modules`

`ln -s /usr/share/eggdrop/scripts /home/eggdrop/scripts`

### Start eggdrop in new user mode -

`eggdrop -m sample.conf`

Now connect to the IRC server and find your bot. In your IRC client, type ‘/msg nameofbot hello‘. The bot will then prompt you to enter a master password and recognise you as the owner.

After setting yourself as master, initiate a DCC chat with the bot. You will be prompted for your password, and then be connected to the bot, where you can administer the bot.

### Add channels that the bot can talk to -

`.chanset #yourchannel +alice`

### To start and stop your bot, first find the process ID of the eggdrop -

`ps aux | grep eggdrop`

Using the PID, type -

`sudo kill PID`

This will shutdown the eggdrop process. To start the eggdrop again, login as user eggdrop (remember, eggdrop will not run as root) and cd to the folder containing the bot’s .conf file and type -

`eggdrop ./sample.conf`
