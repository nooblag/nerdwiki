# Uncomplicated Firewall

Add a rule for limited connections to TCP port only accessible on LAN 

`sudo ufw limit proto tcp from 192.168.0.0/24 to any port 1234`
  
Allow port all protocols from LAN
  
`sudo ufw allow from 192.168.0.0/24 to any port 1234`
