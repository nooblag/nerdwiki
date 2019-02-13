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
        #
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




##NGINX location rewrite URL with or without trailing slash

This location block:

	location = /events {
	    rewrite ^ https://totallydifferenturl.com;
	}

This successfully redirects from mywebsite/events, but I want this block to also handle mywebsite/events/.

You need the ~ operator to enable regex matching, and since you only need to match website/events or website/events/ as full strings, you will need anchors ^ and $ around the pattern:

	location ~ ^/events/?$
	         ^ ^         ^ 

The `^/events/?$` pattern matches:

`^` - start of input

`/events` - a literal substring /events

`/?` - one or zero / symbols

`$` - end of input.
