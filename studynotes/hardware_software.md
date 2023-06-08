## Managing Hardware and Software 

For all things linux hardware and software

### Adding and removing packages 

When installing packages, ubuntu/debian based packages use the apt command whilst redhat based systems use the yum package manager. 

`$ sudo apt/yum install packagename` installs the required package

`$ sudo apt/yum remove packagename` removes the desired package

`$ sudo apt/yum purge packagename` removes packgae with its configuration settings

`$ sudo apt/yum update/upgrade packagename` updates or upgrades package

`$ sudo apt/yum autoremove packagename` removes unwanted/unused packages on a system or those surplus to requirements

`$ sudo apt/yum show packagename` shows packages details incuding version, origin, download size, description and more

`$ sudo apt/yum list packagename` checsk for a newer upgradeable version of package

`$sudo which/whereis packagename` lets you find a package's install location on the machine with whereis offering more info

### Hardware 

`$ lscpu` shows you all cpu and processor information including sockets, threads, cores and more

`$ lshw` lists hardware components connected to the system like memory, usb controllers and network adapters
 
`$ df -h` checks all mounted filesystems

`$ mount | column -t` shows you mounted and unmounted filesystems in nice format

`$ free -m` checks how much free ram you have currently

`$ sudo dmidecode -t processor/bios/memory` lets you access info from the SMBIOS
