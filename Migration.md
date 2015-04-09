# Migration
A basic migration, based on jore's set-up which is based on jl's setup. Pretty much follow this sequence?

`This` is stuff you type.

## 1. Prepare old server

List of config files and other settings that have been customised:

Service | Path to conf and/or other needed files
--- | ---
nginx | /etc/nginx/sites-available/
 | /etc/nginx/ssl/ (certificates)
php5-fpm | /etc/php5/fpm/php.ini
 | /etc/php5/fpm/conf.d/20-apc.ini
mysql | /etc/mysql/my.cnf
exim4 | /etc/exim4/
awstats | /etc/awstats/
 | /var/lib/awstats/
memcached | /etc/memcached.conf
 
This is a good backup line for whole system:

`rsync -aAXvzh --dry-run -e "ssh -p PORT" --exclude={/dev,/proc,/sys,/tmp,/run,/mnt,/media,/lost+found,sysconfig/} user@server:/ /path/to/backup/folder/`
 
#### To have a look at things that have recently been modified:
`ls -larst`
 

### 1.? Dump mysql
`mysqldump -u databaseuser -p databasename > databasename.sql`

---

## 2. New server

### 2.1 SSH Settings
If needed, set up new keys on the local computer you want to hook up to the new server:

`mkdir ~/.ssh`

`chmod 700 ~/.ssh`

`ssh-keygen -t rsa`

Follow the prompts, store as **id_rsa** with no passphrase.

#### Find local key, copy to new server
Run locally: `ssh-copy-id [serveruser]@[sub.domain.com]` (adds keys to 'authorized_hosts', etc)

#### Disable root login
Edit `nano /etc/ssh/sshd_config`

Make sure :/Protocol says "Protocol 2"

##### Enable login only for certain users -

	Authentication:
	LoginGraceTime 120
	PermitRootLogin no
	AllowUsers jl eggdrop jore
	StrictModes yes

##### Change port

#### Reboot
Setup DNS for the new subdomain and reboot. Does key login work okay?

If old key doesn't work, you might need to run `ssh-add`

### 2.? Set up new users and *sudo*
`adduser username`

Set up a home directory if needed.

`mkdir /home/username`

`chown username:users /home/username`

`apt-get install sudo` if sudo not installed.

If you get error about CD, check /etc/apt/sources.list and remove the disc as a source if need be.

Run `visudo` and add this to the list to enable sudo for that user:

`username ALL=(ALL) ALL`

---

### 2.? Run the script?
The script sets up nginx, php-fpm and mysql. At the moment, it's in */root*, run with `bash LEMP*`, follow the prompts, etc.

### 2.? Rsync /var/www/ from old server to new server
`rsync -varlpEAogzhP -e "ssh -p PORT" /var/www/ root@sub.domain.com:/var/www/`

Test with `-n` or `--dry-run` first!

Use *-varlpEAogzhP* as: (v) verbose, (a) archive, (r) recursive, (l) sym links, (p) preserve permissions, (E) preserve the file's executability, (A) preserve ACLs (implies --perms), (o) preserve owner, (g) preserve group, (z) compress, (h) human readable output numbers, (P) keep partially transferred files AND show progress during transfer

#### Also rsync */home* for user data.
`rsync -varlpEAogzhP -e "ssh -p PORT" /home/ root@sub.domain.com:/home/`

### 2.? Setting up mysql

add user, setup the databse and grant permissions

`mysql -u root -p`

> mysql> `create database domain_databasename;`

> mysql> `GRANT ALL PRIVILEGES ON domain_databasename.* TO 'domain_username'@'localhost' IDENTIFIED BY 'PasswordHere';`

Import the SQL dump:

`mysql -u domain_username -p domain_databasename < domain_databasename.sql`

---

## 3. Working?
Check nginx conf

If 403 error, check that nginx is listening for the subdomain properly

---

## ?. Mail (exim4)

`apt-get install exim4`

Make sure `/etc/hostname` `/etc/mailname/` are set to: `sub.domain.com` and that `/etc/hosts` is properly set to point to localhost and sub.domain.com NOT the FQDN. This is so mail can be accepted at the external mailboxes (someone@domain.com) instead of local users.

#### Rsync over confs and settings from old server:
`rsync -varlpEAogzhP -e "ssh -p PORT" /etc/exim4/ root@sub.domain.com:/etc/exim4/`

#### Set up aliases to forward all mail for root to external address:
`nano /etc/aliases`

Edit the file thus:

```
# /etc/aliases
mailer-daemon: postmaster
postmaster: root
nobody: root
hostmaster: root
usenet: root
news: root
webmaster: root
www: root
ftp: root
abuse: root
noc: root
security: root
backup: root
root: someaddress@someotherplace.com
```
#### May need to run configure to set up the new server not to accept any mail locally.
`dpkg-reconfigure exim4-config`

"Internet site; mail is sent and received directly using SMTP" [Enter]

"sub.domain.com" [Enter]

"Listen on 127.0.0.1 ; ::1" [Enter]

Wipe out all other destinations where mail should be accepted. [Enter]

Don't relay mail. [Enter]

#### Working?
`mail -s Test address@domain.com < "This is a test."`

#### Emails from broken crontabs
Check out `cd /etc/cron.d; ls -la` and may need to clean those files up or simply del them.

---

## ?. Setting up Awstats
`apt-get install awstats`

`apt-get install python`

#### Copy confs from:
`rsync -varlpEAogzhP -e "ssh -p PORT" /etc/awstats/ root@sub.domain.com:/etc/awstats/`

#### Copy over record of archived stats
`rsync -varlpEAogzhP -e "ssh -p PORT" /var/lib/awstats/domain.com/ root@sub.domain.com:/var/lib/awstats/domain.com/`

#### Setup awstats to update before log rotate
Some info [here](http://awstats.sourceforge.net/docs/awstats_faq.html#ROTATE), but basically, you add this line `/usr/share/doc/awstats/examples/awstats_updateall.pl now -awstatsprog=/usr/lib/cgi-bin/awstats.pl > /dev/null 2>&1` to */etc/logrotate.d/nginx* which runs before the nginx logs rotate. I like to use /dev/null as this keeps things quiet. Put it in place prerotate so it looks something like:

```nginx
/var/log/nginx/*.log {
        daily
        missingok
        rotate 30
        compress
        delaycompress
        notifempty
        create 0640 www-data adm
        sharedscripts

        #email a copy of the log to here
        #mail someone@domain.com

        prerotate
                #jore - run perl script that updates ALL awstats configs before rotating logs, old single domain below commented out
                /usr/share/doc/awstats/examples/awstats_updateall.pl now -awstatsprog=/usr/lib/cgi-bin/awstats.pl > /dev/null 2>&1
                #/usr/lib/cgi-bin/awstats.pl -config=domain.com -update -dir=/dev/null

                if [ -d /etc/logrotate.d/httpd-prerotate ]; then \
                        run-parts /etc/logrotate.d/httpd-prerotate; \
                fi \
        endscript

        postrotate
                [ ! -f /run/nginx.pid ] || kill -USR1 `cat /run/nginx.pid`
        endscript
}
```

#### Remove the awstats cron since we're doing log rotate instead
`rm /etc/cron.d/awstats`

#### Install IP and GeoIPFree plugins for awstats
`apt-get install libnet-ip-perl libgeo-ipfree-perl`

#### Working?
Check in browser to see if all is working and awstats does dynamic compile by clicking on the "Update now" link.

---

## ?. Setting new server timezone
`dpkg-reconfigure tzdata`

Verify with:

`date`

##### Setting time and date
`date -s "31 Mar 2015 18:00:00"`

---

## ?. Install fail2ban
`apt-get install fail2ban`

---

## ?. Change login banner

Move old file as backup, `sudo mv /etc/motd /etc/motd.bak`

Create new `/etc/motd` file (post-login message), save.

Add/edit following line in `/etc/default/rcS` -- `EDITMOTD=no`

`sudo nano /etc/ssh/sshd_config` and uncomment the Banner line with `/etc/issue.net`

`sudo nano /etc/issue.net` -- displayed on connect, pre-login

`sudo nano /etc/motd` -- displayed post-login

have a look at `/etc/update-motd.d/00-header` (whats going on there?)

`/etc/init.d/ssh restart` if done properly, won't all disappear on reboot!

---

## Fiddle with memcached
Used notes [here](http://www.pontikis.net/blog/install-memcached-php-debian) for initial setup, although this was for Apache.

#### Prerequisites 
Just rsync over *my.cnf* (there's custom settings in there for mysql which get used for memcached) and the rest in terms of handling and parsing is done in nginx confs that already exist. A sample config is [here](http://download.kyup.com/wordpress/conf.d) though. Wordpress requires the [nginx cache optimizer plugin](https://wordpress.org/plugins/nginx-cache-optimizer/) to use memcached.

`apt-get install memcached`

After installed, `nano /etc/memcached.conf` and check it. You may need to rsync older conf if any changes.

Need to also install PHP extension: `apt-get install php5-memcached`

---

## Backup ideas
#### Backup user
Remove default backup user: `userdel -r backup` and clear out any other default users that are not wanted too, if you like, such as *games*, *news*, etc.

#### Cronic
May want to [investigate](http://habilis.net/cronic/) *cronic* if crontab emails become annoying (more than likely).

`wget https://mrkmg.com/install_cronic.sh` and run `sh install_cronic.sh`

Make sure *make* is executable: `chmod 755 make`

#### Add the *make* bash script to crontab
We want to run the *make* script every arvo at around 5:30pm, our time (should also be localserver time, check this is set and clocks are the same!), as 5:30pm AUD is the offpeak time for site according to logs from *awstats*.

Edit crontab for backup user `crontab -u backup -e`, add this:
```
30 17 * * * cronic /location/of/backup/make
```

Also set another cronjob to cleanup any sqldumps that are over certain age. One on server side to cleanup every 14 days, another on remote side to cleanup maybe every two months. Time starts at 7:13pm. Make sure this is very much after *./backup/make* can be finished.

Example -- 7:13pm, on 1st and 15th days of each month:

`13 19 1,15 * * cronic find /location/of/backup/*.tar.gz -mtime +14 -delete`

Example -- 7:15pm, on 1st day of every other month (*/2):

`13 19 1 */2 * cronic find /location/of/backup/*.tar.gz -mtime +60 -delete`

##### If you get 'sdin not tty' kind of error at remote host:
Add the following to *.bashrc* file in homedir: `[[ $- != *i* ]] && return`

---
