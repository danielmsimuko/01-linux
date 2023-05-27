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

$ tar -cvzf archname.tar.gz /dir/filetoarch -- creates an archive of file to archive
$ tar -tf archname.tar.gz -- list what is in the archived files
$ tar -tf myapp.tar.gz > app.list -- redirect archive output into a file

$ ls -l /etc | less -- lists etc dir with more info 
$ cat file1.csv | sort | head -10 -- cat out file 1 sort it and output only the first 10 lines 
$ ls -l /etc > etclist.txt -- list out etc dir and output into file etclist. can overwrite any existing file
$ ls -l /etc >> etclist.txt -- creates or appends file if already exists
$ cat /etc 2> /dev/null -- sends error messages 2 to dev/null black hole

$ sudo less +F /var/log/syslog -- less continues in bground + updates in real time 

## Linux Bootloader + Processes

The bootloader is the hub of the operating system. Responsible for loading the kernel of the operating system into memory and then transferring control to it. Most common linux bootloader is GRUB2.

### Kernel and Runtime

`$ sudo sysctl -a` checks the current parameter configurations for the operating system


$ sysctl dev.cdrom.autclose -- returns dev parameter specs
$ sudo sysctl -w dev.cdrom.autoclose=0 -- autoclose parameter changed
$ cd /etc/sysctl.d/ -- contain master values for kernel parameters
$ shutdown -P/-r/-H -- performs the poweroff, reboot or halt command to shutdown system 
$ sudo shutdown -r now -- immediate reboot (replace now with mins  i.e +5)
$ systemctl get-default -- finds the runlevel of machine for systemd
$ uptime -- low long the system has been up 
$ runlevel -- finds how long the current runlevel is for sysVinit
$ vim /boot/grub/grub.cfg -- where the grub config is
$ sudo update-grub -- updates the bootloader
$ grub-mkconfig -o /boot/grub/grub.cfg -- updating grub in centos

----------UPDATING AND MANAGING SOFTWARE----------
$ sudo apt/yum install -- installs a package  
$ sudo apt/yum remove -- removes a package 
$ sudo apt/yum purge -- removes packgae with configuration 
$ sudo apt/yum update/upgrade -- updates and upgrades package 
$ sudo apt/yum autoremove -- removes unwanted packages 
$ sudo apt/yum show -- shows packages details
$ sudo apt/yum list -- upgradeable
$ sudo apt/yum httpd -- searches for httpd package

----------ADDING USERS + GROUPS----------
$ su - username -- login as someone else
$ sudo useradd (name) -- adding a user to system
$ sudo userdel (name) -- delete a user
$ sudo passwd (name) -- give the user a password 
$ sudo usermod -s /bin/bash (name) -- bin bash
$ sudo mkhomedir_helper (name) -- creates home dir for user 
$ sudo useradd -m (name) -- quicker way of adding user acc
$ cat /etc/skel -- boilerplate user adding files 
$ sudo groupadd (grp name) -- adds a new group
$ sudo usermod -a -G (grpname) (username) -- adds a user to a group
$ sudo visudo -- edit the sudoers 
$ sudo cat /etc/sudooers -- shows people and groups who can sudo
$ for i in name1 name2 ... ; do sudo useradd -m $i ; done -- add mult-users
$ for i in grp1 grp2 ... ; do sudo usermod -a -G $i name1 name2 ...; done -- adding multi user to multi-grp





----------PROCESSES + TASK SHEDULING-----------
$ top/htop -- displays all processes
$ ps -ef -- shows all processes running on the pc
$ ps aux --forest | grep cron -- filters process to get cron information
$ crontab -l -- view crontabs for task sheduling 
$ crontab -e -- edit your crontab
# min (m), hour (h), day of mon (dom), month (mon), day of week (dow), use '*' for 'any'
-- */3 * * * * echo "Awake" >> /home/daniel/logs/system_awake.log -- runs every 3 mins, any h,dom,mon,dow logs awake in sys awake file
$ less /var/log/syslog | grep -i cron -- for checking if cron is running



----------REGEX----------
$ grep '^$ sudo' lcsa.txt -- searches every line that starts with $ sudo
$ grep '\<[tT]he\>' lcsa.txt -- returns every instance of word 'the'
$ grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-za-z]{2,6}\b" lcsa.txt -- finds email address in file i.e x@gmail.com

----------THE NETWORKING STUFF----------
$ ip route show -- shows us the routing table and gateway server
$ ip addr show -- ip address and also mac address 
$ ifconfig -- displays status of current and active interfaces
$ netstat -- lists active internet connections 
$ nmcli -- network manager for linux
$ cat /etc/services | grep 22 -- finds all services using port 22
$ cat /etc/services | grep 53 -- finds all services using port 53
$ cat /etc/resolv.conf | grep nameserver -- finds dns server
$ host www.website.com -- performs dns lookup
$ dig www.website.com -- performs dns lookup with more info 
$ ping -c1 www.acloudguru.com -- test connectivity to website 
$ curl -i www.acloudguru.com -- tests connectivity to website 

----------HARDWARE----------
--memtest86 -- can be completed from the GRUB menu 
--NEVER CHECK MOUNTED FILE SYSTEM
$ df -h -- check all mounted filesystems
$ sudo umount /file/path/data -- mount point has been removed 
$ sudo  fsck /file/path -- check bios
$ sudo tune2fs -c 0 /file/path -- check shedule and reboot
  
----------BASIC SECURITY----------
michael@ubuntu:-$ -- standard user permissions 
root@ubuntu:-# -- root user acess 
$ su (username) -- change user to another  
$ cat /etc/sudoers -- list of users who have sudo commands 
$ cat /etc/group | grep daniel -- finds groups user daniel is in
$ cat /etc/passwd | grep root -- finds info on root. UID=0
# cat /etc/shadow -- can find hash of user passwords
# groups daniel -- shows you all groups user daniel is in
$ getent passwd daniel -- determines users home shell

----------LOGGING + SCRIPTING----------
$ export PATH=$PATH:/path/to/scriptsdir
$ sudo less /var/log/(logname) | grep (keyword) -- log info from file and filters for keywords
$ sudo less /var/log/syslog -- system info
$ sudo less /var/log/auth.log -- authentication log, esp when users >1
$ (if statement structure) -- if {a = b}; then echo True else echo False fi
$ (for loop structure) -- for x in 1 2 3 do echo "some info" done

----------BONUS----------
$ ssh cloud_user@pub.lic.ip.adr -- ssh into a linux machine
$ sudo systemctl start/stop (service) -- starts stops service like mysql
$ cd /temp -- for when you need to stage files in a temporary folder 
$ sudo apt install httpd -- shows a list of webservers you can install 
$ sudo apt install apache2 -- installs apache2 webserver
$ sudo systemctl start/stop/status apache2  -- starts/stops/status apache2 server status
$ code/vim /var/www/html/index.html -- where the file can be found
$ uptime -- checks how long the server has been up for. 

####STUFF////

$ ps aux | grep -v grep | wc -l -- return number of running processes 
$ cat /proc/loadavg -- retuns current system load
$ ps -U (username) | wc -l -- returns number of processes running as (username)
$ ps aux | grep (processname) -- returns process info 
$ ps aux | grep (processname) | grep -v grep -- returns a value for the PID
$ cat /proc/(pid_value)/status | grep Threads  -- returns number of threads a process is using

-----2. VIEWING SERVICE LOGS

$ curl -I localhost --
$ sudo cat /var/log/httpd/access_log | grep -E "^(PRIV-IP)" | wc -l --
$ curl http://(PUBLIC-IP)/index.html -- 
$ sudo tail -f /var/log/httpd/access_log -- see who accessed the sever
$ curl http://(PUBLIC_IP)/server.html --

 
DATA STORAGE
$ cat /var/log/syslog -- application logging for deb based systems
$ cat /var/log/auth.log  -- authentication logs
$ cat /var/log/secure -- for redhat based systems
$ cat /var/log/boot.log -- sytem boot logs 
$ cat /var/log/cron.log -- cron jobs log 
$ cat /var/log/kern.log -- kernel logs
$ cat /var/log/faillog.log -- authentication failure log

COMPUTER NETWORKING
$ ip addr show -- lists the ip addresses
$ ping -c 1 google.com -- pings a network address
$cat /etc/hosts -- info about all ip connections.
$ cat /etc/resolv.conf -- gets the host nameserver
$ dig www.linuxacademy.com -- resolves dns name



$ which python -- finds where programme python is stored 
$ whereis apache2 | tr " " '\n' -- finds apache2 and pipes + translates info into readable lines 







