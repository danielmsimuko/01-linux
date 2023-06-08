
## Networking and Troubleshooting Notes

`$ ip route show` shows us the routing table and gateway server

`$ ip addr show` shows us a more information on ip address and procides mac addresses 

`$ ifconfig` displays status of current and active interfaces like netmask, broadcast address and more

`$ netstat` prints network connections and routing tables

`$ sudo apt/yum install metwork-manager` installs a network manager for linux

`$ cat /etc/services | grep portnumber` finds all services using designated port number

`$ cat /etc/resolv.conf | grep nameserver` gets you the nameserver ip address

`$ dig/host www.websitename..com` performs dns lookup

`$ ping www.websitename..com` tests the connectivity of a website

`$ cat /etc/hosts` gets information about current ip connections

`$ dig www.linuxacademy.com` is a tool for looking up DNS name servers
