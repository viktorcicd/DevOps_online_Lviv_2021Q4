Configure network devices on VM1, VM2
```
sudo ip addr add 192.168.1.4/24 dev enp0s3  on VM2
sudo ip addr add 192.168.1.1/24 dev enp0s8  on VM1
ip link set dev enp0s3 up  on VM2
ip link set dev enp0s8 up  on VM1

sudo route add default gw 192.168.1.1 enp0s3  on VM2

nameserver 8.8.8.8 added to /etc/resolv.conf  on VM2
```
Enable forwarding on VM1
```
sudo nano /etc/sysctl.conf 
net.ipv4.ip_forward = 1
sysctl -p  to make changes take effect
iptables -t nat -A POSTROUTING -t nat -s 192.168.1.0/24 -o enp0s3 -j MASQUERADE
```
 
3.Check the route from VM2 to Host. 
```
traceroute -I 192.168.31.163
```
4.Check the access to the Internet, (just ping, for example, 8.8.8.8). 
```
ping google.com
```
5.Determine, which  resource has an IP address 8.8.8.8.
```
nslookup 8.8.8.8
```
6.Determine, which  IP address belongs to resource epam.com. 
```
nslookup epam.com
```
7.Determine the default gateway for your HOST and display routing table. 
```
route print
```

8.Trace the route to google.com. 
```
mtr google.com
```
![linux](./images/1.png "linux")
 
![linux](./images/2.png "linux")
  
![linux](./images/vm.png "linux")

![linux](./images/94.png "linux")

![linux](./images/95.png "linux")

![linux](./images/96.png "linux")

![linux](./images/97.png "linux")

![linux](./images/98.png "linux")

![linux](./images/99.png "linux")

![linux](./images/100.png "linux")

 

