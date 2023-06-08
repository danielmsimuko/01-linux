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
