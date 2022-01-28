Lets install and configure VM3

Install and configure dhcp server
```
sudo apt-get install isc-dhcp-server
nano /etc/dhcp/dhcpd.conf
nano /etc/default/isc-dhcp-server

default-lease-time 7200;
max-lease-time 43200;

subnet 192.168.1.0 netmask 255.255.255.0 {

range 192.168.1.2 192.168.1.100;

option routers 192.168.1.1;

option domain-name-servers 192.168.1.1;
```


