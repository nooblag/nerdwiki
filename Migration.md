# Migration
A basic migration, based on thmb. Pretty much follow this sequence?

`This` is stuff you type.

## 1. Prepare old server

Fetch the following config files and other settings:

Service | Path to conf and/or other needed files
--- | ---
nginx | /etc/nginx/sites-available/
 | /etc/nginx/ssl/ (certificates)
php | ?? php.ini
exim4 | /etc/exim4/
awstats | /etc/awstats/
 | /var/lib/awstats/
 
This is a good backup line for whole system:

`rsync -aAXrvzhn -e "ssh -p PORT" --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found", "sysconfig/"} root@sub.domain.com:/ /home/n/Projects/domain/backups/NAMEOFHOST/`
 
### 1.? Have a look at things that have recently been modified:
`ls -larst`
 

### 1.? Dump mysql
`mysqldump`

---

## 2. New server

### 2.1 SSH Settings
If needed, set up new keys on the local computer you want to hook up to the new server:

`mkdir ~/.ssh`

`chmod 700 ~/.ssh`

`ssh-keygen -t rsa`

Follow the prompts, store as **id_rsa** with no passphrase.

#### Find local key, copy to new server
Run locally: `ssh-copy-id [serveruser]@[sub.domain.com]`

#### Add keys to 'authorized_hosts'

#### Disable root login
Edit `nano /etc/ssh/sshd_config`

Make sure :/Protocol says "Protocol 2"

#### Change port

#### Reboot
Setup DNS for the new subdomain and reboot. Does key login work okay?

### 2.? Set up new users and sudo
`adduser username`

Set up a home directory if needed.

`mkdir /home/username`

`chown username:users /home/username`

`apt-get install sudo` if sudo not installed.

Run `visudo` and add this to the list to enable sudo for that user:

`username ALL=(ALL) ALL`

---

### 2.? Run the script?
The script sets up nginx, php-fpm and mysql?

### 2.? Rsync /var/www/ from old server to new server
`rsync -varlpEAogzhP -e "ssh -p PORT" /var/www/ root@sub.domain.com:/var/www/`

Test with `-n` or `--dry-run` first.

Use *-varlpEAogzhP* as: (v) verbose, (a) archive, (r) recursive, (l) sym links, (p) preserve permissions, (E) preserve the file's executability, (A) preserve ACLs (implies --perms), (o) preserve owner, (g) preserve group, (z) compress, (h) human readable output numbers, (P) keep partially transferred files AND show progress during transfer

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

---

## ?. Setting up Awstats
`apt-get install awstats python`

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
#### Install IP and GeoIPFree plugins for awstats
`apt-get install libnet-ip-perl libgeo-ipfree-perl`

#### Working?
Check in browser to see if all is working and awstats does dynamic compile by clicking on the "Update now" link.

---

## ?. Setting new server timezone
`dpkg-reconfigure tzdata`

Verify with:

`date`

---

## ?. Install fail2ban
`apt-get install fail2ban`
