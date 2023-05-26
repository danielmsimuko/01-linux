# LFCSA
Study Notes for Linux Foundation Certified Sys Administrator

## Basics of File Manipulation

### Editing files + Directories 
`$ touch filename.txt` creates a text file in the current working directory. To check which directory you are in type `$ pwd`

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

$ cmp file1 file2 -- returns the first diff between files
$ stat filename -- gets the statistics for file 
$ lsattr filename -- check if file is immutable 
$ sudo chattr +i start.sh -- adds immutable attribute. for removal, use -i

### File and Directory Permissions 

Directory permissions take the form `drwxr-xr-x` --for directories 
-rwxr-xr-x -- for files  
$ sudo su - username -- become the user 
$ id (username) -- view user permissions 
$ sudo chown (username) (filename) -- change a files ownership
$ sudo chown : (grpname) (filename) -- changes a files group ownership
$ sudo chmod 644 (filename) -- changes file permissions numerically 
$ sudo chown -R usename1:groupname1 /home/deleteduser1 -- changing ownership recursively
$ sudo chown username:grpname -- changes ownership of group 
$ find /dirnam/appnam -name "d*" -ok chmod 660 {} \; -- find app in dir, with name beginning d, change permissions and execute with confirmation
$ find /home -nouser -nogroup -exec chown username:grpname {} \; -- find directory not owned by user or group and changes it to specified user/grp


### F 

### G

$ tar -cvzf archname.tar.gz /dir/filetoarch -- creates an archive of file to archive
$ tar -tf archname.tar.gz -- list what is in the archived files
$ tar -tf myapp.tar.gz > app.list -- redirect archive output into a file

$ ls -l /etc | less -- lists etc dir with more info 
$ cat file1.csv | sort | head -10 -- cat out file 1 sort it and output only the first 10 lines 
$ ls -l /etc > etclist.txt -- list out etc dir and output into file etclist. can overwrite any existing file
$ ls -l /etc >> etclist.txt -- creates or appends file if already exists
$ cat /etc 2> /dev/null -- sends error messages 2 to dev/null black hole




$ sudo less +F /var/log/syslog -- less continues in bground + updates in real time 
 




----------BOOTING----------
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

----------BASICS----------
$ cat filename.txt  -- output file in terminal
$ more filename.txt -- output file in terminal 
$ less filename.txt -- advance output one screen at time. less can find names
$ sudo less +F /var/log/syslog -- less continues in bground + updates in real time 
$ cat filename.csv | more -- displays info on screen with more flexibility
$ touch filename.txt -- create an empty file 
$ diff -c file1 file2 -- compares 2 fil or dir line by line with context
$ diff ../dir/ ../dir2/ -- dir 1 and dir 2 compared 
$ comm file1 file2 -- compares files. must be sorted
$ cmp file1 file2 -- returns the first diff between files
$ stat filename -- gets the statistics for file 
$ lsattr filename -- check if file is immutable 
$ sudo chattr +i start.sh -- adds immutable attribute. for removal, use -i 





----------PROCESSES + TASK SHEDULING-----------
$ top/htop -- displays all processes
$ ps -ef -- shows all processes running on the pc
$ ps aux --forest | grep cron -- filters process to get cron information
$ crontab -l -- view crontabs for task sheduling 
$ crontab -e -- edit your crontab
# min (m), hour (h), day of mon (dom), month (mon), day of week (dow), use '*' for 'any'
-- */3 * * * * echo "Awake" >> /home/daniel/logs/system_awake.log -- runs every 3 mins, any h,dom,mon,dow logs awake in sys awake file
$ less /var/log/syslog | grep -i cron -- for checking if cron is running

----------SYSTEMS, KERNEL AND RUNTIME----------
$ sudo sysctl -a -- current parameter configurations. returns every parameter configured on system
$ sysctl dev.cdrom.autclose -- returns dev parameter specs
$ sudo sysctl -w dev.cdrom.autoclose=0 -- autoclose parameter changed
$ cd /etc/sysctl.d/ -- contain master values for kernel parameters

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







