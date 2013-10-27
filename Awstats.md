Notes for setting up Awstats with Nginx, running on Debian 7 (Wheezy).

Assumes Awstats already installed and a config setup with `cp /etc/awstats/awstats.conf /etc/awstats/awstats.www.example.com.conf`, and also Nginx config already set up for Awstats on a subdomain---for example, stats.example.com.

These pages were very helpful:
http://www.bytetouch.com/blog/system-administration/how-to-awstats-installation-and-configuration-on-debian/
http://www.rubynginx.com/index.php/2012/10/02/setup-awstats-phpmyadmin-phppgadmin-with-nginx-on-ubuntu/
http://kamisama.me/2013/03/20/install-configure-and-protect-awstats-for-multiple-nginx-vhost-on-debian/


## Create a php script to handle all requests to /cgi-bin.

Since Awstats needs `http://stats.example.com/cgi-bin/awstats.pl`, we need to create a php script that is passed requests via php-fcgi.

Create new file
`nano /etc/nginx/cgi-bin.php`

And put this in it:
`<?php

$descriptorspec = array(
    0 => array("pipe", "r"),  // stdin is a pipe that the child will read from
    1 => array("pipe", "w"),  // stdout is a pipe that the child will write to
    2 => array("pipe", "w")   // stderr is a file to write to
);

$newenv = $_SERVER;
$newenv["SCRIPT_FILENAME"] = $_SERVER["X_SCRIPT_FILENAME"];
$newenv["SCRIPT_NAME"] = $_SERVER["X_SCRIPT_NAME"];

if (is_executable($_SERVER["X_SCRIPT_FILENAME"])) {
    $process = proc_open($_SERVER["X_SCRIPT_FILENAME"], $descriptorspec, $pipes, NULL, $newenv);
    if (is_resource($process)) {
        fclose($pipes[0]);
        $head = fgets($pipes[1]);
        while (strcmp($head, "\n")) {
            header($head);
            $head = fgets($pipes[1]);
        }
        fpassthru($pipes[1]);
        fclose($pipes[1]);
        fclose($pipes[2]);
        $return_value = proc_close($process);
    } else {
        header("Status: 500 Internal Server Error");
        echo("Internal Server Error");
    }
} else {
    header("Status: 404 Page Not Found");
    echo("Page Not Found");
}
?>`

Then chmod:
`chmod +x /etc/nginx/cgi-bin.php`


## Setting nginx log formats for awstats

Change nginx’s log format to match apache so awstats can read it properly:
`nano /etc/nginx/nginx.conf`

Find this line:
`include       /etc/nginx/conf/mime.types;`

And paste this in below it:
`log_format main     '$remote_addr - $remote_user [$time_local] "$request" '
                    '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent" "$http_x_forwarded_for"';`
                    
                    
## Nginx configs

must modify the domains nginx config file and add the cgi-bin redirect so that it sends them to our php script from above.

`nano /etc/nginx/sites-available/example.com`

Find this `location ~ .php$ {` and paste the following BEFORE it:
`location ^~ /awstats-icon {
    alias /usr/share/awstats/icon/;
    access_log off;
}

location ^~ /awstatscss {
    alias /usr/share/doc/awstats/examples/css/;
    access_log off;
}

location ^~ /awstatsclasses {
    alias /usr/share/doc/awstats/examples/classes/;
    access_log off;
}

# Configure /cgi-bin/scripts to go through php-fastcgi
location ~ ^/cgi-bin/.*\.(cgi|pl|py|rb) {
    gzip off;
    fastcgi_pass  127.0.0.1:49232;
    fastcgi_index cgi-bin.php;
    fastcgi_param SCRIPT_FILENAME    /etc/nginx/cgi-bin.php;
    fastcgi_param SCRIPT_NAME        /cgi-bin/cgi-bin.php;
    fastcgi_param X_SCRIPT_FILENAME  /usr/lib$fastcgi_script_name;
    fastcgi_param X_SCRIPT_NAME      $fastcgi_script_name;
    fastcgi_param QUERY_STRING       $query_string;
    fastcgi_param REQUEST_METHOD     $request_method;
    fastcgi_param CONTENT_TYPE       $content_type;
    fastcgi_param CONTENT_LENGTH     $content_length;
    fastcgi_param GATEWAY_INTERFACE  CGI/1.1;
    fastcgi_param SERVER_SOFTWARE    nginx;
    fastcgi_param REQUEST_URI        $request_uri;
    fastcgi_param DOCUMENT_URI       $document_uri;
    fastcgi_param DOCUMENT_ROOT      $document_root;
    fastcgi_param SERVER_PROTOCOL    $server_protocol;
    fastcgi_param REMOTE_ADDR        $remote_addr;
    fastcgi_param REMOTE_PORT        $remote_port;
    fastcgi_param SERVER_ADDR        $server_addr;
    fastcgi_param SERVER_PORT        $server_port;
    fastcgi_param SERVER_NAME        $server_name;
    fastcgi_param REMOTE_USER        $remote_user;
}`

Restart nginx `service nginx restart` and see what happens.

When you installed AWStats it installed it’s own cron in your cron.d, we need to delete this as it will just continue to error (we are using separate configs per domain and don’t need the default.)
`rm /etc/cron.d/awstats`


## Generating the stats

Command to generate simple static stats (index.htm):
`/usr/lib/cgi-bin/awstats.pl -config=www.example.com -update -output > /www/sites/www.example.com/index.htm`

But this will only create main reports. To create all reports, you can use `awstats_buildstaticpages.pl`.  That file is at: `/usr/share/awstats/tools/awstats_buildstaticpages.pl`

So, set up a file to run the command that calls `awstats_buildstaticpages.pl` using:
`nano /etc/awstats/update`

Insert:
`/usr/share/awstats/tools/awstats_buildstaticpages.pl -update -config=www.example.com -dir=/www/sites/stats.example.com/ -awstatsprog=/usr/lib/cgi-bin/awstats.pl`

Updating can be done from cron, but that can result in lost data, because of log rotation. Best option is to call update script just before logs are rotated. Nginx logs are, by default, rotated daily, so we can just insert our script in nginx logrotate configuration file (/etc/logrotate.d/nginx):

/var/log/nginx/*.log {
    daily
    ...
    sharedscripts
    prerotate
        /etc/awstats/update
    endscript
    ...
}

`chmod +x /etc/awstats/update`

----

More to do, but for now you can try to run logrotate manually with:
`logrotate -vf /etc/logrotate.conf`


