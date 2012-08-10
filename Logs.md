## Monitor a log

Use `tail` -

`sudo tail -f /var/log/messages`

`sudo tail -f /var/log/auth.log`

## Logwatch

Emails a summary of logs, set with a cronjob.

`sudo aptitude install logwatch`

Edit `/usr/share/logwatch/default.conf/logwatch.conf` and change variables to your liking.

Add a crontab to email at certain times -

`0 7 * * * /usr/sbin/logwatch`

## Awstats

Stolen from http://www.bytetouch.com/blog/system-administration/how-to-awstats-installation-and-configuration-on-debian/

Using Nginx.

Install Awstats -

`sudo aptitude install awstats`

Create a config file for the domain -

`cp /etc/awstats/awstats.conf /etc/awstats/awstats.www.example.com.conf`

Edit the new config file and change these lines accordingly -

    LogFile="/var/log/nginx/access.www.example.com.log"
    LogFormat=1
    SiteDomain="www.example.com"
    DNSLookup=0
    DirData="/var/lib/awstats/www.example.com/"
    HostAliases="example.com"

Create a database directory -

`mkdir /var/lib/awstats/www.example.com/`

Generate a stats page -

`/usr/lib/cgi-bin/awstats.pl -config=www.example.com -update -output > /var/www/www.example.com/awstats.html`

This will only create main reports.

## Misc

### Seach logs for SSH connections

`grep -w 'sshd' /var/log/auth.log | grep -w 'Accepted' | awk '{ print $0 }'`
