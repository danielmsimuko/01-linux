## User Management 

### Adding users 

`sudo adduser username` will create an account, home directory and prompt you for a password. This is a newer feature and isnt available on all linux distros

`$ su - username` allows you to switch to another user

`$ sudo useradd -m -s /bin/bash username` adding a user to system while setting the home directory + default shell  

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

### Environment Variables 

You can have three types of environment variables: `local`, `user` + `sysem` variables

> Local 
variables relating to the current session only 

> User
variables that would be related to the user only

> System Wide
System wide would be available to all users and on the system at all times

`$ env` prints out the current variable 

`$ echo MY_VAR` creates a variable 

`unset MY_VAR` removes that variable 
