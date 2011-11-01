## Installing Wordpress

`wget http://wordpress.org/latest.tar.gz`

`tar xzvf latest.tar.gz`

`sudo mv wordpress /var/www/nameofblog`

`cd /var/www/nameofblog`

`sudo mv wp-config-sample.php wp-config.php`

`sudo nano wp-config.php`

Add details of mysql table for blog, mysql username and password. Then goto blog in browser to finish installation.

## Moving blog to new server

Follow instructions from Wordpress site -

http://codex.wordpress.org/Moving_WordPress

http://codex.wordpress.org/Backing_Up_Your_Database

http://codex.wordpress.org/Restoring_Your_Database_From_Backup

### Make blog directory owner and group 'www-data', same as user running Apache.

CHMOD all directories 755, all files 644 -

`find [your path here] -type d -exec chmod 755 {} \;`

`find [your path here] -type f -exec chmod 644 {} \;`

`chmod 777 wp-content/uploads`

### Change URLs in MySQL with PHPMyAdmin

Click on blog database, then wp_options

Run SQL command -

`UPDATE wp_options SET option_value = replace(option_value, 'http://www.old-domain.com', 'http://www.new-domain.com') WHERE option_name = 'home' OR option_name = 'siteurl';`

Click wp_posts, run SQL command -

`UPDATE wp_posts SET guid = replace(guid, 'http://www.old-domain.com','http://www.new-domain.com');`

and -

`UPDATE wp_posts SET post_content = replace(post_content, 'http://www.old-domain.com', 'http://www.new-domain.com');`

### Errors and workarounds

May have to adjust Permalinks in Wordpress settings if clicking on categories and posts leads to a 404 error after a move. 
