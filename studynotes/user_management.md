## User Management 

### Adding users 

`sudo adduser username` will create an account, home directory and prompt you for a password. This is a newer feature and isnt available on all linux distros

`$ su - username` allows you to switch to another user

`$ sudo useradd -m -s /bin/bash username` adding a user to system while setting the home directory + default shell  

`$ sudo userdel username` deletes a user

`$ sudo passwd username` assigns a user a password

`# echo Temp@$$ | passwd --stdin username` assigns a temp password for user which they will need to change at next logon

`chage -d0 username` forces a password change at next logon

`$ sudo usermod -(#)` modifies a users characteristics using -m, -p, and more

`$ sudo groupadd grpname` adds a new group

`$ sudo chgrp grpname filename` changes the group ownership of a file 

`$ sudo usermod -a -G grpname username` adds a user to a group

`$ sudo visudo ` lets you edit the sudoers file which grands sudo permissions to users

`$ for i in name1 name2 ... ; do sudo useradd -m $i ; done` is a for loop to add more than one user at a time

`$ for i in grp1 grp2 ... ; do sudo usermod -a -G $i name1 name2 ...; done` adds multiple users to user to multi-group

`$ sudo cat /etc/sudoers` lists which users have sudo commands 

`$ sudo cat /etc/shadow` finds the hash string of a users password 

### Environment Variables 

You can have three types of environment variables: `local`, `user` + `sysem` variables

Local variables relate to the users current session only, user variables to the user in every session and system wide for all users in every session 

System wide would be available to all users and on the system at all times

`$ env` prints out the current variable 

`$ echo MY_VAR` creates a variable 

`unset MY_VAR` removes that variable 

### Configure user limits 

There are 2 types of files for linux administrators to perform : Hard and Soft 

`$ /etc/security/limits.conf` is the main file that can achieve this. 

Inside the file is the parameters that can determine limits to users

`domain` which can be user, group name, etc

`type` whcih can have either soft or hard for the limit type

`item` which is the item to limit, can be a file, process, fsize etc...

`value` the value you are setting for the limit 

To view which limits are defined for the system `$ ulimit -a`

### User Priviledges

To manage remote access `$ vim /etc/security/access.conf`

File is arranged as `permission : users : origins` where +/- adds and removes access, users can contain users/groups or all and lastly origins which is where users can connect from which could be a hostname, domain name, ipaddress...


### Configure PAM - Pluggable Authentication Modules 

Allows you to configure and reconfigure how authentication takes place 

`$ vim /etc/pam.conf` file can be used to configure on local machine or series of files in `$ cd /etc/pam.d` directory

Three columns required for pam entry: `module` for authentication account, password or session 

