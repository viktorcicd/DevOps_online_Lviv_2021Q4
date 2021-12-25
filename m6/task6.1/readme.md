 iptables -t nat -A PREROUTING -p tcp –dport 80 -j DNAT –to-destination 122.164.34.240. 
 iptables -t nat -A POSTROUTING -p tcp -d 122.164.34.240 –dport 80 -j MASQUERADE
