## Basics

List all crontabs -

`crontab -l`

New crontab -

`crontab -e`

## Format

`m h dom mon dow commandtorun`

1. Minute
2. Hour
3. Day of month
4. Month
5. Day of week

then command to run.

Example to create backup of home folder every night @ 4:20am - 

`20 4 * * * tar -zcf /mnt/files/jlhomebak.tgz /home/jl/`

## Run cron job on reboot

`@reboot echo hello`

## Run job every 5 minutes

`*/5 * * * * echo hello`

## Cool crontabs

Turn screensaver on every night @ 3am -

`0 3 * * * xset s on`
