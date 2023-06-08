## Logging and Scripting 

Scripting and logging is an essential part of troubleshooting. Any information regarding processes will have a log stored somewhere on the system with the common area being the `/var/log` directory. Below are a few commands that help find and use this information

`$ sudo less /var/log/(logname) | grep (keyword)` is used log info from file and filters for keywords

`$ sudo less /var/log/syslog` is the command to get the syslog information printed within terminal

`$ sudo less /var/log/auth.log` outputs authentication log info and can be grep'd using a keyword

`$ cat /var/log/secure` for redhat based systems

`$ cat /var/log/boot.log` is the location where system boot logs are located

`$ cat /var/log/cron.log` is where the cron jobs logging reside

`$ cat /var/log/kern.log` kernel logs are found here

`$ cat /var/log/faillog.log` logs authentication failures on the system 

### Scripting 

`$ if condition; then condition fi` is the common structure on which if statements are built on 

`$ for condition in condition do action done` is the structure for for loops within bash scripting

## Regular Expression 

Regex expressions take the novice/intermediate linux user to an advanced user of the OS. These commands allow for precise searching of files, directories and precise instructions for administration tasks. Combined with common linux actions and a powerful text editor such as Vim, the command line can become the most powerful place to be. 

`$ grep '^$ sudo' filename` searches every line that starts with $ sudo in the file

`$ grep '\<[tT]he\>' filename` returns every instance of word 'the' within filename

`$ grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-za-z]{2,6}\b" filename` outputs all email address in file i.e x@gmail.com
