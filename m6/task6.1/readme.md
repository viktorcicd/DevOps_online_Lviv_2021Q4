 ip address add 192.168.1.200/255.255.255.0 dev eth0
 
![linux](./images/1.png "linux")
 
![linux](./images/2.png "linux")
  
![linux](./images/vm.png "linux")

![linux](./images/ip add.png "linux")
 
 iptables -t nat -A PREROUTING -p tcp –dport 80 -j DNAT –to-destination 122.164.34.240. 
 iptables -t nat -A POSTROUTING -p tcp -d 122.164.34.240 –dport 80 -j MASQUERADE
