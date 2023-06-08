## SELinux and AppAromour

SELinux stands for security enhanced linux and is a kernel module for more secure access control and security policies. It is used within redhat/centos systems

`$ getenforce` checks the current mode of SElinux 

`$ setenforce` set the selinux mode to either enforcing or permissive

`$ sudo semanage fcontent -l` contains all context information for every file, directory and process information

`$ ls /file/dir -Z` checks for file contexts within desired directory

`$ ps auxZ | grep cron` filters out the process policies for cron through grep filter

AppArmour is a kernal enhancement usd to confine applications to a select set of resources. This is pathbased so it simpler and easier to learn. This is common on ubuntu/debian based systems 

`$ aa-enabled` returns whether apparmor is enabled 

`$ aa-disable` will disable apparmor security profile

`$ aa-complain` will set an apparmor security profile to complain mode 

`$ sudo aa-status` checks the status of apparmor on the machine. these include profiles/processes in enforce and complaint mode

`$ sudo /etc/apparmor.d` directory is where apparmor resides within ubuntu based systems

`$ cat /etc/apparmor.d/lxc-default` is the default directory which should never be edited

`$ cat /etc/apparmor.d/lxc-containers` is the place where you would set up apparmor controls 

### Packet Filtering 

`$ sudo iptables -l` views current configurations 

`$ sudo iptables --flush` refreshes current config so admin can start afresh

`$ sudo iptables -A INPUT --protocol icmp --in-interface ens5 -J REJECT/DROP` lets you implement packet filter to prevent access to machine 


