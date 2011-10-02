## Misc errors and fixes

## If .php pages aren't showing and are offering to download the files instead.

Edit /etc/apache2/mods-enabled/php5.conf to match the following -

	<IfModule mod_php5.c>
	<FilesMatch "\.ph(p3?|tml)$">
	SetHandler application/x-httpd-php
	</FilesMatch>
	<FilesMatch "\.phps$">
	SetHandler application/x-httpd-php-source
	</FilesMatch>
	# To re-enable php in user directories comment the following lines
	# (from <IfModule ...> to </IfModule>.) Do NOT set it to On as it
	# prevents .htaccess files from disabling it.
	#<IfModule mod_userdir.c>
	# <Directory /home/*/public_html>
	# php_admin_value engine Off
	# </Directory>
	#</IfModule>
	</IfModule> 
