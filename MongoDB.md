## Install

`sudo aptitude install mongodb`

### With PHP extension

`git clone whatever`

`make install`

.. and all that. Obviously update this.

## Querying

### Search all

`db.members.find()`

### Insert an item

`db.members.insert( { name: "Dave", lastName: "Grohl", instrument: "Vox/Guitar" } )`

### Update an item

`db.members.update( { lastName: "Grohl" }, { "$set" : { "instrument" : "Vox/Guitar" } } } )`

### Remove an item

`db.members.remove( { name: "Dave" } )`
