## Setting a static IP for a network interface

Edit network interfaces file -

`sudo nano /etc/network/interfaces`

	This file describes the network interfaces available on your system
	and how to activate them. For more information, see interfaces(5).

	The loopback network interface

		auto lo
		iface lo inet loopback

	The primary network interface

	auto eth0
		iface eth0 inet static
		address 192.168.0.100
		netmask 255.255.255.0
		network 192.168.0.0
		broadcast 192.168.0.255
		gateway 192.168.0.1

### Restart networking for changes to take effect -

`sudo /etc/init.d/networking restart`
