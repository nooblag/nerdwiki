## Basics

Add a new box to Vagrant -

`vagrant box add name_of_box path_to_box`

Remove a box from Vagrant -

`vagrant box remove name_of_box`

Initialize a new box in new directory -

`vagrant init box_name`

Start up a box -

`vagrant up`

SSH to a box -

`vagrant ssh`

Pause a running box -

`vagrant suspend`

Resume a paused box -

`vagrant resume`

Wipe an initialized box -

`vagrant destroy`

## Creating a new base box

From - http://vagrantup.com/docs/base_boxes.html

Based on Debian Squeeze 32-bit ISO.

Basic requirements - 

* VirtualBox Guest Additions
* SSH key-based authentication
* Ruby and RubyGems to install Chef and Puppet
* Chef and Puppet for provisioning support

### Steps to create new box -

* Create new VM in VirtualBox. Allocate 40gb dynamic disk space.

* Allocate 384mb RAM (default setting). Can always change this later.

* Disable audio, USB controllers, other un-needed stuff.

* Ensure NAT is enabled.

* Boot install disc. Use these settings -

* Hostname: vagrant-debian-squeeze
* Domain: vagrantup.com
* Root pass: vagrant
* Main user: vagrant
* Main user pass: vagrant

Do not install GUI or guest additions from Debian installer.

* Remove installation CD from apt sources in `/etc/apt/sources.list` and run `aptitude update`

* Boot VM, login as user. Run `aptitude install sudo`

* Run `visudo`. Change the `env_keep` line at top of file to match the below -

`Defaults  env_keep+=SSH_AUTH_SOCK`

And add the following line to allow passwordless sudo for members of the `admin` group - 

`%admin ALL=NOPASSWD: ALL`

* Add the `admin` group with `groupadd admin`

* Add `vagrant` user to `admin` group with `usermod -aG admin vagrant`

* Restart sudo with `/etc/init.d/sudo restart`

* Run `aptitude install ruby-dev rubygems puppet`

* Run `sudo gem install chef --no-rdoc --no-ri`

* Run `sudo apt-get install linux-headers-$(uname -r) build-essential`

* Mount Guest Additions in GUI under Devices.

* Run `sudo mount /dev/cdrom /media/cdrom`

* Run `sudo sh /media/cdrom/VBoxLinuxAdditions.run` to install Guest Additions.

* Add `UseDNS No` to `/etc/sshd_config` to speed up SSH connections.

* Run `apt-get clean` to clear cache and free up space.

* Under `vagrant` user, add the key from the following link to `~/.ssh/authorized_keys` and ensure file is chmod `0600` -

`https://raw.github.com/mitchellh/vagrant/master/keys/vagrant.pub`

* Package the new box using the VirtualBox VM name -

`vagrant package --base my_base_box`

This will make a new file named package.box

* Add `package.box` to Vagrant - 

`vagrant box add my_box package.box`

* Start up the new box -

`cd test_environment`

`vagrant init my_box`

`vagrant up`

`vagrant ssh`
