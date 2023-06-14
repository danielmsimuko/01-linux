## Service configuration 

### Caching DNS server 

DNS resoution is a key component of a network/service environment. As a sys-admin, its important to provide reliable dns responsiveness 

Basic DNS zone configuration checklist: 

check to see if BIND is installed -  install if neccesary 

configure bund using `/etc/bind/named.cinf.options` but loction of file might differ 

check configuration using `named-checkconf`

restart BIND using `systemctl`
