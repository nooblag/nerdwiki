## SQLite3

### Install

`sudo aptitude install sqlite3 php5-sqlite`

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

## MySQL

### Create new user

`CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'newpassword';`

### Grant access to a DB to new user

`GRANT ALL PRIVILEGES ON somedb.* TO 'newuser'@'localhost' WITH GRANT OPTION;`

### Import a .sql file to DB

From CLI - 

`mysql -u user -p -h localhost nameofdb < file.sql`
