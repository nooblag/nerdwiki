## Install
`sudo aptitude install mongodb`

### With PHP extension

`git clone whatever`

`make install`

.. and all that. Obviously update this.

## Querying

### Search all

`db.members.find()`

### Updating an item

`db.members.update( { lastName: "Grohl" }, { "$set" : { "instrument" : "Vox/Guitar" } } } )`
