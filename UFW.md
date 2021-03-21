# Uncomplicated Firewall

Allow limited connections to a TCP port only accessible through LAN

`sudo ufw limit proto tcp from 192.168.0.0/24 to any port 1234`
  
Allow connections to a port, all protocols, only accessible through LAN
  
`sudo ufw allow from 192.168.0.0/24 to any port 1234`
