# MySQL

## Example usages

### List current databases
`mysql -u root -p`

`show databases;`

### Create new database
`CREATE DATABASE nameOfDatabase;`

### Create new user

`CREATE USER 'newUser'@'localhost' IDENTIFIED BY 'newPassword';`

### Grant access to a DB to new user

`GRANT ALL PRIVILEGES ON nameOfDatabase.* TO 'newUser'@'localhost' WITH GRANT OPTION;`

### Work with certain database
`USE nameOfDatabase;`

### Insert a row into a table

`INSERT INTO nameOfTable (nameOfColumn1, nameOfColumn2) VALUES ("value1", "value2");`

### Update a row in a table

`UPDATE nameOfTable SET nameOfColumn="valueToChangeTo" WHERE nameOfIdColumn="rowId";`

### Delete a row in a table

`DELETE FROM nameOfTable WHERE nameOfIdColumn="rowId";`

### Deleting junk
`SELECT * FROM `_posts` WHERE `post_status` = "inherit" LIMIT 0 , 3000`

`DELETE FROM `dbname`.`_posts` WHERE `post_status` = "inherit";`

`DELETE FROM `dbname`.`_postmeta` WHERE `_postmeta`.`meta_key` = "enclosure";`

### Find/Replace text inside post
`UPDATE _posts set post_content = replace(post_content, 'Before', 'After')`

#### Change to archive from
`UPDATE _postmeta set meta_value = replace(meta_value, 'CURRENT_VALUE', 'CHANGE_TO_THIS');`

#### Replace meta_values for ATOM FEED -- 'enclosure' custom feild
`UPDATE _postmeta set meta_value = replace(meta_value, 'CURRENT_VALUE', 'CHANGE_TO_THIS');`

### Search all posts contents for something using wildcard
`SELECT *  FROM `dbname`.`_posts` WHERE `post_content` LIKE '%http://content.server.com/video/%.jpg%'`

`SELECT *  FROM `dbname`.`_posts` WHERE `post_content` LIKE '%file="http://content.server.com/%.mp4%' AND `post_status` = "publish";`

### Reset views stats:
`UPDATE _postmeta SET meta_value = '0' WHERE meta_key = "views"`

### Turn off search engines
`UPDATE _options SET option_value = 0 WHERE option_name = "blog_public"`


### List all titles:
`SELECT `post_title` FROM `_posts` WHERE 1 AND `post_type` LIKE 'post' AND `post_status` LIKE 'publish' LIMIT 0 , 3000`

### Move install from server to server, check SQLS for ref to old links:

`UPDATE _options SET option_value = replace(option_value, 'http://server.com', 'http://0.0.0.0') WHERE option_name = 'home' OR option_name = 'siteurl';`

`UPDATE _posts SET guid = replace(guid, 'http://server.com', 'http://0.0.0.0');`

`UPDATE _posts SET post_content = replace(post_content, 'http://server.com', 'http://0.0.0.0'); `

## Backups

### Backup a MySQL database

`mysqldump -u nameOfUser -p nameOfDatabase > nameOfBackupFile.sql`

### Restore a database from backup

`mysql -u nameOfUser -p -h localhost nameOfDatabase < nameOfBackupFile.sql`

# SQLite3

## Example usages

### Create a new database

`sqlite3 new.db`

### Create a new table

`create table newtable (ids integer primary key, Date text, Start text, End text, Distance text);`

### List all tables

`.tables`

### Insert a value into a table

`insert into newtable (Date) values ('06/01/12');`

### Insert multiple values

`insert into newtable values(1, '06/01/12', 'Home', 'Breakwall', '10.42km');`

### List all data in a table

`select * from newtable;`
