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
exim4 | ??
awstats | /etc/awstats/
 | /var/lib/awstats/
 

### 1.1 Dump mysql
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
Run locally: `ssh-copy-id [serveruser]@[subdomain.thoughtm.com]`

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
`rsync -varlpEAogzhP -e "ssh -p PORT" /var/www/ root@subdomain.thoughtm.com:/var/www/`

Test with `-n` or `--dry-run` first.

Use *-varlpEAogzhP* as: (v) verbose, (a) archive, (r) recursive, (l) sym links, (p) preserve permissions, (E) preserve the file's executability, (A) preserve ACLs (implies --perms), (o) preserve owner, (g) preserve group, (z) compress, (h) human readable output numbers, (P) keep partially transferred files AND show progress during transfer

### 2.? Setting up mysql

add user, setup the databse and grant permissions

`mysql -u root -p`

> mysql> `create database thoughtm_databasename;`

> mysql> `GRANT ALL PRIVILEGES ON thoughtm_databasename.* TO 'thoughtm_username'@'localhost' IDENTIFIED BY 'PasswordHere';`

Import the SQL dump:

`mysql -u thoughtm_username -p thoughtm_databasename < thoughtm_databasename.sql`

---

## 3. Working?
Check nginx conf

If 403 error, check that nginx is listening for the subdomain properly

---

## ?. Mail (exim4)

`apt-get install exim4`

Make sure `/etc/hostname` `/etc/mailname/` are set to: `subdomain.thoughtm.com` and that `/etc/hosts` is properly set to point to localhost and subdomain.thoughtm.com NOT the FQDN. This is so mail can be accepted at the external mailboxes (someone@thoughtm.com) instead of local users.

---

## ?. Setting up Awstats
`apt-get install awstats python`

Copy confs from:
rsync -varlpEAogzhP -e "ssh -p PORT" /etc/awstats/ root@subdomain.thoughtm.com:/etc/awstats/

record of stats
rsync -varlpEAogzhP -e "ssh -p PORT" /var/lib/awstats/thoughtm.com/ root@subdomain.thoughtm.com:/var/lib/awstats/thoughtm.com/


Check for the thing that rotates logs cos that's where you put the awstats command (what is it) to run every night

---

## ?. Setting new server timezone
`dpkg-reconfigure tzdata`

Verify with: `date`
