## MacBook Air 4,2 (Mid 2011)

### Install Debian Wheezy 7.0

- Partition drive, format as free space
- Install refit, sync partitions
- Boot from Apple Superdrive (would not boot with any other drive). Also use Apple Ethernet USB adapter
- Install, choose advanced for bootloader and shell. Use largest continuous free space. Use ext4 for better SSD support. Seperate /home folder
- Install bootloader to / partition only. Get this through shell with mount
- Resync partitions with refit
- Boot Debian
