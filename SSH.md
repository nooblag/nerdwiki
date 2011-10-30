## Secure SSH server
`sudo nano /etc/ssh/sshd_config`

Disable root login and enable login only for certain users

	Authentication:
	LoginGraceTime 120
	PermitRootLogin no
	AllowUsers jl eggdrop jore
	StrictModes yes

Change SSH port from 22 to something else
	
	What ports, IPs and protocols we listen for
	Port 14666

## SOCKS5 proxy

`ssh -p 14666 -D 8082 user@123.156.156.23`

## Tunnel port on remote machine to local machine

E.g. Mysql port located on a remote server and forward to local port. From local machine -

`ssh user@domain.org -L 1900:localhost:3306`

## Reverse tunnel

On remote machine, SSH with -

`ssh -R 19999:localhost:22 user@123.156.156.23` (port 19999 can be any unused port)

On local machine, SSH with -

`ssh localhost -p 19999`

## Reverse VNC tunnel

On remote server, run -

`ssh user@otherserver.net -R 5900:127.0.0.1:5900`

then on local client, connect to VNC on localhost via port 5900

## Password-less SSH

To enable password-less SSH login between two machines, a public key (id_rsa.pub) must be generated on your home machine and then uploaded to a remote machine. This will enable you to log in to the remote machine and not be prompted for a password.

To generate an id_rsa.pub file, open up a terminal and type the following:

`ssh-keygen -t rsa`

Just press ‘enter’ for all of the following prompts:

	Generating public/private rsa key pair.
	Enter file in which to save the key (/home/user/.ssh/id_rsa):
	Enter passphrase (empty for no passphrase):
	Enter same passphrase again:
	Your identification has been saved in /home/user/.ssh/id_rsa.
	Your public key has been saved in /home/user/.ssh/id_rsa.pub.

This will leave the passphrase empty, enabling password-less login.

Now that the public key file has been generated it needs to be transferred to the remote machine that we want to log in to. You can use rsync, scp, FTP, or anything similar, just as long as the id_rsa.pub file that was generated is transferred to ~/.ssh/authorized_keys on the remote server. Here’s a few examples:

* `scp ~/.ssh/id_rsa.pub user@domain.com:.ssh/authorized_keys`
* `rsync --progress -e ssh ~/.ssh/id_rsa.pub user@domain.com:.ssh/authorized_keys`
* `ssh-copy-id -i ~/.ssh/id_rsa.pub user@domain.com`

Once id_rsa.pub has been transferred, try to SSH to the remote server. If everything went OK then you shouldn’t be prompted for a password.

If it dosen’t work, either the SSH configuration on the remote machine isn’t set up to accept public keys and password-less logins, or the permissions of the id_rsa.pub file are incorrect. Google is your friend here, and also this link has some helpful hints (http://www.debian-administration.org/articles/152).

## Change ssh login banner etc

move old file as backup, `sudo mv /etc/motd /etc/motd.bak`

create new `/etc/motd` file (post-login message), save.

add/edit following line in `/etc/default/rcS` -- `EDITMOTD=no`

`sudo nano /etc/ssh/sshd_config` and uncomment the Banner line with `/etc/issue.net`

`sudo nano /etc/issue.net` -- displayed on connect, pre-login

`sudo nano /etc/motd` -- displayed post-login

have a look at `/etc/update-motd.d/00-header` (whats going on there?)

`/etc/init.d/ssh restart` if done properly, won't all disappear on reboot!

## Running remote commands

Works best to have a public key setup between the two servers.

`ssh user@server.net ls`

## Run multiple commands -

`ssh user@server.net "/home/user/scripts/lol.sh; ls"`

## Share SSH connections

Useful if you have several SSH sessions open to the same server. This
will use the existing SSH connection for all other connections. It makes
things really fast.

Edit or create `~/.ssh/config` file and add the following -

    Host *
      ControlMaster auto
      ControlPath ~/.ssh/master-%r@%h:%p

chmod the file 600.

## AutoSSH

Keeps a SSH connection alive. Requires SSH key for passwordless login.

E.g. creates a reverse SSH tunnel from local port 22 to remote port 1984, using port 29001 to monitor the SSH connection for connectivity. The `-f` option makes autoSSH a daemon.

`autossh -M 29001 -f -N -R 1984:localhost:22 user@hostname.org`

`autossh -M 29001 -f -N -R 1901:localhost:22 jl@leagueofevil.org`

Use a cronjob to run command every 2 minutes (just to be sure). Add to crontab -

`*/2 * * * * autossh -M 29001 -f -N -R 1984:localhost:22 user@hostname.org`
