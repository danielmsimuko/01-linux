## Service configuration 

DNS is the contact list for the internet. If you have a domain, rather than using ip addressing, we will configure the files so that the addresses are translated into a string that we can reference. 

For example, one of the most common websites `google.com` also has a popular ipaddress in `8.8.8.8`

DNS resoution is a key component of a network/service environment. As a sys-admin, its important to provide reliable dns responsiveness. 

### Caching DNS server 

Basic DNS zone configuration checklist: 

check to see if BIND is installed -  install if neccesary 

configure bund using `/etc/bind/named.cinf.options` but loction of file might differ 

check configuration using `named-checkconf`

restart BIND using `systemctl`


#### install 

`$ sudo apt install bind9 bind9utils bind9-doc` installs bind9 

You can edit the `named.conf.optiond` file to configure 

`$ named-checkconf` command will check the configuration and will not output anything if no errors arise

`$ sudo systemctl restart bind9` restarts the service so changes to the config file are picked up 

### Maintaining a DNS zone

Components of a DNS zone include a zone entry in the `named.conf` file along with forward lookup zone file and reverse lookup zone file. 

Zone files can contain some of the following pieces: start of authority (soa) , name server (ns), A record (a), mail for exchange (mx) and a canonical name or alias(cn)

the `named.conf.local` file is the one you would need to start editing 

`sudo named-checkzone la.local /etc/bind/fewd.la.local.db` ia the command needed after editing the la.local file

`dig (targetserver)` is also another command you can use 






