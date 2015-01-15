Tested on Debian Squeeze and Wheezy.

Based on and stolen from - http://www.howtoforge.com/installing-nginx-with-php5-and-mysql-support-on-debian-squeeze

## Install

`aptitude install nginx`

### Install PHP5 with SQLite module - 

`aptitude install php5-cgi php5-mysql php5-curl php5-gd php5-idn php-pear php5-imagick php5-imap php5-mcrypt php5-memcache php5-ming php5-pspell php5-recode php5-snmp php5-sqlite php5-tidy php5-xmlrpc php5-xsl`

Open `/etc/php5/cgi/php.ini` and uncomment the line `cgi.fix_pathinfo=1`

Run `aptitude install lighttpd; update-rc.d -f lighttpd remove; /etc/init.d/lighttpd stop`

Edit `/etc/rc.local` and add the following line just before the `exit` line in the file -

`/usr/bin/spawn-fcgi -a 127.0.0.1 -p 9000 -u www-data -g www-data -f /usr/bin/php5-cgi -P /var/run/fastcgi-php.pid`

.. also run line as a command to start FastCGI process.

### Config

Edit `/etc/nginx/nginx.conf` - 

        worker_processes  5;
        keepalive_timeout  2;

Make a new `/etc/nginx/sites-enabled/host.conf` file with your hostname -

        server {
        
            server_name  YOUR_HOSTNAME_HERE;
            access_log  /var/log/nginx/localhost.access.log;

            location / {
                root  /var/www;
                index  index.php index.html index.htm;
            }

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
            location ~ \.php$ {
                fastcgi_pass   127.0.0.1:9000;
                fastcgi_index  index.php;
                fastcgi_param  SCRIPT_FILENAME  /var/www$fastcgi_script_name;
                include         fastcgi_params;
        }

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        location ~ /\.ht {
                deny  all;
        }
        }

Finally, restart nginx with `/etc/init.d/nginx restart`

## Errors and workarounds

Ensure ownership on `/var/www` is correct - `chown www-data:www-data /var/www`

Check configs with `nginx -t`

## Some SSL Stuff

Still new to this and fiddling, but something useful so far:

        server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/domain.crt;
        ssl_certificate_key /etc/nginx/ssl/domain.key;
        keepalive_timeout   70;
        
        #jore - enables all versions of TLS, but not SSLv2 or 3 which are crap and now deprecated.
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        
        #jore - disable weak ciphers
        ssl_ciphers "ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-SHA384:ECD$
        ssl_prefer_server_ciphers on;
        }
        

## Awstats!
Jore: I can't really remember how I got this working. Woops. But this is current nginx conf for awstats subdomain as of Debian 7:

        server {
        ...
        #jore - include fcgiwrap for use with awstats later
        include /etc/nginx/fcgiwrap.conf;
        
        location / { index index.php index.htm index.html; error_page 404 /; }
        location ^~ /awstats-icon { alias /usr/share/awstats/icon/; }
        location ^~ /awstatscss { alias /usr/share/doc/awstats/examples/css/; }
        location ^~ /awstatsclasses { alias /usr/share/doc/awstats/examples/classes/;  }
        
        location = /cgi-bin/awstats.pl {
                #jore - require a login for awstats
                auth_basic "Login for Awstats";
                auth_basic_user_file  /etc/awstats/awstats.domain.com.htpasswd;
                
                #jore - set doc root to where awstats is installed which is at /usr/lib/cgi-bin/awstats.pl
                root /usr/lib;
                gzip off;
                
                #jore - setup fastcgi support for awstats (to handle the awstats.pl from browser---makes dynamic stats)
                include /etc/nginx/fastcgi_params;
                fastcgi_pass unix:/var/run/fcgiwrap.socket;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
