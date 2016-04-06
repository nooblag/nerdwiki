## General

`tcpdump -nnvvXS`

## Specific port & interface

`tcpdump -i en3 port 80`

## Display for only source (not destination) with specific protocol

`tcpdump -i en3 src port 80 and tcp`
