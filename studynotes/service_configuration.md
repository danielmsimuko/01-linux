## Service configuration 

### Caching DNS server 

DNS resoution is a key component of a network/service environment. As a sys-admin, its important to provide reliable dns responsiveness 


Basic DNS zone configuration checklist: 

check to see if BIND is installed -  install if neccesary 

configure bund using `/etc/bind/named.cinf.options` but loction of file might differ 

check configuration using `named-checkconf`

restart BIND using `systemctl`


### install 

`$ sudo apt install bind9 bind9utils bind9-doc` installs bind9 

You can edit the `named.conf.optiond` file to configure 

`$ named-checkconf` command will check the configuration and will not output anything if no errors arise

`$ sudo systemctl restart bind9` restarts the service so changes to the config file are picked up 
