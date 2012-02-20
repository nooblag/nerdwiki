### List all processes -

`ps aux`

### List process named 'apache' -

`ps aux | grep 'apache'`

### Pause a process -

`Ctl-Z`

### List stopped or background jobs; resume a stopped job in the background -

`bg` 

### Bring most recent job to the foreground -

`fg`

### Bring job `n` to the foreground -

`fg n`

### Logout a user

As root -

`pkill -KILL -u nameofuser`

### Get output of process

Find pid -

`ps aux|grep dd`

Send USR1 to process -

`kill -USR1 pidofprocess`

This will print an output to STDOUT.
