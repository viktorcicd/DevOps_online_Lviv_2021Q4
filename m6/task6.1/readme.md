sudo ip addr add 192.168.1.4/24 dev enp0s3
sudo ip addr add 192.168.1.1/24 dev enp0

![linux](./images/1.png "linux")
 
![linux](./images/2.png "linux")
  
![linux](./images/vm.png "linux")

![linux](./images/ip add.png "linux")
 
 iptables -t nat -A PREROUTING -p tcp –dport 80 -j DNAT –to-destination 122.164.34.240. 
 iptables -t nat -A POSTROUTING -p tcp -d 122.164.34.240 –dport 80 -j MASQUERADE
