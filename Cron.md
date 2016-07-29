## Basics

### List all crontabs

`crontab -l`

### New crontab

`crontab -e`

### Wipe all jobs from crontab

`crontab -r`

## Format of crontab

`m h dom mon dow COMMAND_TO_RUN`

1. `m` = Minute
2. `h` = Hour
3. `dom` = Day of month
4. `mon` = Month
5. `dow` = Day of week

## Example crontabs

### Run job on reboot

`@reboot echo hello`

### Run job every 5 minutes

`*/5 * * * * echo hello`

### Turn screensaver on every night @ 3am

`0 3 * * * xset s on`

### Create backup of home folder every night @ 4:20am

`20 4 * * * tar -zcf /mnt/files/jlhomebak.tgz /home/jl/`
