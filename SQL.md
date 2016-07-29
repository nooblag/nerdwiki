# MySQL

## Example usages

### Create new user

`CREATE USER 'newUser'@'localhost' IDENTIFIED BY 'newPassword';`

### Grant access to a DB to new user

`GRANT ALL PRIVILEGES ON nameOfDatabase.* TO 'newUser'@'localhost' WITH GRANT OPTION;`

### Insert a row into a table

`INSERT INTO nameOfTable (nameOfColumn1, nameOfColumn2) VALUES ("value1", "value2");`

### Update a row in a table

`UPDATE nameOfTable SET nameOfColumn="valueToChangeTo" WHERE nameOfIdColumn="rowId";`

### Delete a row in a table

`DELETE FROM nameOfTable WHERE nameOfIdColumn="rowId";`

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
