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
