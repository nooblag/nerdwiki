## Installing phpMyAdmin

`apt-get install phpmyadmin`

Set apache2 virtual host or redirect to `/usr/share/phpmyadmin`

OR create a symbolic link to `/var/www` directory. First navigate to `/var/www`, then -

`ln -s /usr/share/phpmyadmin phpmyadmin`
