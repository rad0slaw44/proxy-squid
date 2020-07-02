# **PROXY-SQUID (OHMP)**

This repository contains the configuration files for proxy squid service running on EC2 instances. (OHMP environment)
The purpose of this project was to limit the access through proxy only to the specified destination URLs.

The repository consists of the squid configuration files for the child proxy and the parent proxy as well as the "child-allowed-sites.acl" file that contains
the URLs allowed to be accessed through the child proxy server. Parent proxy is deployed for each customer. 
In addition there is a "*CustomerName*-parent-allowed-sites.acl file for each customer. 

- child-proxy - child proxy configuration file
- parent-proxy - parent proxy configuration file
- child-allowed-sites.acl - allowed URLs on the child proxy.
- *CustomerName*-parent-allowed-sites.acl - allowed URLs for the specyfic customer.

Both child and parent proxy files are configured to allow the access only to the destinations specyfied in the "allowed-sites.acl" file.
Any other access through proxy is denied and logged in /var/log/squid/access.log. This is achived be the following lines in the configuration file.

- `acl allowed_urls dstdomain "/etc/squid/allowed-sites.acl"`  #ACL definition

- `http_access allow allowed_urls` #ACL application


All the `localnet` ACL entries as well as the `http-access` entry refering to "localnet" ACL have been commented out.
*******