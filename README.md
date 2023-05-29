# Linux Foundation Certified System Administrator 
These are my study notes for the Linux Foundation Certified System Administrator Exam. They comprise of the bulk of the commands I have come across. At a more advanced level, these commands become longer, more complex but more powerful.

These notes will be expanded upon as my knowledge bases continues to grow so I hope they provide some value to you. 

See if you know what this command does: 

`$ grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-za-z]{2,6}\b" filename.txt`  

## Basics
These notes assume you are already familiar with Linux and are comfortable enough to at least move between directories. Commands such as `$ cd /dirname` , `$ clear` and `$ exit` are already familiar to you. If not, it would be worth investing time into learning the essentials via the Linux Professional Institutes Essentials Course.

### Editing files + Directories 
`$ touch filename.txt` creates a text file in the current working directory. To check which directory you are in enter `$ pwd`

To go to the home directory `$ cd ~`

`$ vim filename.txt` lets you edit the file. You can also use `$ nano filename.txt` to do so 

`$ cat filename.txt` outputs contents of file in the terminal

You can also use `$ more filename.txt` which advances one screen at a time or `$ less filename.txt` which can be more consise if used with `$ less filename.txt | grep filter`

`$ cp file1 newfile2` duplicates a files contents

`$ mv filename /file/path/filename` can move files from one directory to another

`$ mkdir /dir/path/dirname` makes a new directory in specified location

`$ rm /path/to/dir/filename` removes the file from the specified directory

`$ rm -rf /path/to/dir` deletes a directory without warning 

`$ sudo find /dirname -name "filename"` searches for a file by name in your chosen directory

`$ sudo find /dirname -type f -name "*.type"` searches for all files ending with .type in your chosen directory. This can be .txt .log .html and more

`$ sudo find /dirname -type f -user username` searches for files in chosen directory owned by user username 

### File Comparisons and Statistics  

`$ diff -c filename1 filename2` command contextually compares the two files line by line

`$ diff /dirname1 /dirname2` compars directories one and two for differences

`$ comm filename1 filename2` compares files in sorted order

`$ cmp filename1 filename2` simply returns the first difference it can find between files. Common to use for almost identical files

`$ stat filename` gives you information of the file including size, access date and read write permissions

`$ lsattr filename` lists the files attributes

`$ sudo chattr [-pRVf] filename` adds file attributes to filename with several optional 

### File and Directory Permissions 

`$ sudo su - username` allows you to log into machine as another user

`$ id username`allows you to view user permissions

Directory permissions take the form `drwxr-xr-x` and file permissions take the form `-rwxr-xr-x`

`$ ls -l` lists the contents of a directory including its file permissions with `ll -l` offering more information including hidden files

`$ sudo chown username filename ` changes the ownership of a filename to username

`$ sudo chown groupname:filename` changes the group ownership of a file to group

`$ sudo chmod 644 filename` changes file permissions numerically -  NOTE: most common numerical permissions are 777,  755,  644 and 660

`$ sudo chown -R usename1:groupname1 /home/deleteduser1` -- changing ownership recursively if assigning permissions to a deleted user

`$ sudo chown username:grpname` changes ownership of group

More complex problem solving can then be attained through layering commands together such as: 

`$ find /dirnam/appnam -name "d*" -ok chmod 660 {} \;` which finds an application name beginning with letter d, within specified directory, changes the permissions to 660 and asks for confirmation. 

`$ find /dirname -nouser -nogroup -exec chown username:grpname {} \;` finds files in directory not owned by any user OR any group and changes this to the specified user and group 

### Archiving Files 

`$ tar -cvzf archname.tar.gz /dir/filename` creates an archive of filename

`$ tar -tf archname.tar.gz` list what is in the archived files

`$ tar -tf myapp.tar.gz > app.list`redirects archive output into a file which can then be catted or filtered using grep

`$ ls -l /etc > etclist.txt` list out etc dir and output into file etclist but can be overwritten

`$ ls -l /etc >> etclist.txt` creates or appends file if already exists

## Linux Bootloader + Processes

The bootloader is the hub of the operating system. Responsible for loading the kernel of the operating system into memory and then transferring control to it. Most common linux bootloader is GRUB2.

### Kernel and Runtime

`$ vim /boot/grub/grub.cfg` is where the grub config resides 

`$ sudo update-grub` updates the bootloader after the config changes

`$ grub-mkconfig -o /boot/grub/grub.cfg` updating grub in CentOS/RedHat based system

`$ sudo sysctl -a` checks the current parameter configurations for the operating system

`$ runlevel` finds how long the current runlevel is for sysVinit

`$ systemctl get-default` finds the runlevel of the machine for systmd 

`$ uptime` shows you how long the system has been up 

`$ cd /etc/sysctl.d/` contain master values for kernel parameters

`$ shutdown -P/-r/-H` performs the poweroff, reboot or halt command to shutdown system

`$ sudo shutdown -r now` does an immediate reboot (replace now with mins  i.e +5)

### Processes and Task Sheduling 

`$ top/htop` displays all processes currently running on machine 

`$ ps -ef` shows all processes running on the machine 

`$ ps aux --forest | grep cron` filters process to get cron information. Cron can be replaced with another filter

`$ crontab -l` views the users crontabs for task sheduling 

`$ crontab -e` allows user to edit the crontab

Crontab works so that the digits represent the: `min (m), hour (h), day of mon (dom), month (mon), day of week (dow)`. Any woould be '*'

A great example is the following sheduled task below: 

`*/3 * * * * echo "Awake" >> /home/daniel/logs/system_awake.log` 

This script rns every 3 mins, every/any hour, any day of month, month of year, day of week and logs the echo command "Awake" inside the /home directory and stored in the file system_log.awake. 

`$ less /var/log/syslog | grep -i cron` outputs contents of syslog and checks for cron process

`$ ps aux | grep -v grep | wc -l` return the total number of running processes

`$ cat /proc/loadavg` retuns the current system load

`$ ps -U (username) | wc -l` returns number of processes running by/for (username)

`$ ps aux | grep (processname)` returns process info

`$ ps aux | grep (processname) | grep -v grep` returns a value for the PID

`$ cat /proc/(pid_value)/status | grep Threads` returns number of threads a process is using. Can be helpful in determining what processes are using up computering resources

## Managing Hardware and Software 

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

## User Management 

### Adding users 

`$ su - username` allows you to switch your user to another 

`$ sudo useradd username` adding a user to system

`$ sudo userdel username` deletes a user

`$ sudo passwd username` assigns a user a password

`$ sudo usermod -(#)` modifies a users characteristics using -m, -p, and more

`$ sudo groupadd grpname` adds a new group

`$ sudo usermod -a -G grpname username` adds a user to a group

`$ sudo visudo ` lets you edit the sudoers file which grands sudo permissions to users

`$ for i in name1 name2 ... ; do sudo useradd -m $i ; done` is a for loop to add more than one user at a time

`$ for i in grp1 grp2 ... ; do sudo usermod -a -G $i name1 name2 ...; done` adds multiple users to user to multi-group

`$ sudo cat /etc/sudoers` lists which users have sudo commands 

`$ sudo cat /etc/shadow` finds the hash string of a users password 

## Networking and Troubleshooting

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

## Logging and Scripting 

$ export PATH=$PATH:/path/to/scriptsdir
$ sudo less /var/log/(logname) | grep (keyword) -- log info from file and filters for keywords
$ sudo less /var/log/syslog -- system info
$ sudo less /var/log/auth.log -- authentication log, esp when users >1
$ (if statement structure) -- if {a = b}; then echo True else echo False fi
$ (for loop structure) -- for x in 1 2 3 do echo "some info" done

$ curl -I localhost --
$ sudo cat /var/log/httpd/access_log | grep -E "^(PRIV-IP)" | wc -l --
$ curl http://(PUBLIC-IP)/index.html -- 
$ sudo tail -f /var/log/httpd/access_log -- see who accessed the sever
$ curl http://(PUBLIC_IP)/server.html 
$ cat /var/log/syslog -- application logging for deb based systems

$ cat /var/log/auth.log  -- authentication logs
$ cat /var/log/secure -- for redhat based systems
$ cat /var/log/boot.log -- sytem boot logs 
$ cat /var/log/cron.log -- cron jobs log 
$ cat /var/log/kern.log -- kernel logs
$ cat /var/log/faillog.log -- authentication failure log

## Regular Expression 

$ grep '^$ sudo' lcsa.txt -- searches every line that starts with $ sudo
$ grep '\<[tT]he\>' lcsa.txt -- returns every instance of word 'the'
$ grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-za-z]{2,6}\b" lcsa.txt -- finds email address in file i.e x@gmail.com

## Randomers

$ cd /temp -- for when you need to stage files in a temporary folder 

$ sudo systemctl start/stop/status apache2  -- starts/stops/status apache2 server status
$ code/vim /var/www/html/index.html -- where the file can be found. 
$ which python -- finds where programme python is stored 
$ whereis apache2 | tr " " '\n' -- finds apache2 and pipes + translates info into readable lines 





