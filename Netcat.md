Install netcat -

`sudo aptitude install netcat`

## Simple chat server

On server -

`nc -l -p 3333`

On client -

`nc <server> 3333`

On server, pipe to `pv` for data transfer information -

`nc -l -p 3333 | pv -b`
