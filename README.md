# **PROXY-SQUID (OHMP)**

This repository contains the configuration files for proxy squid service running on EC2 instances. (OHMP environment)
The purpose of this project was to limit the access through proxy only to the specified destination URLs.

## CHILD PROXY (opti-ohmp-jmp1)

The child proxy is configured to allow the user traffic as long as the user comes from the valid source AND the traffic is going to the allowed origin AND the user is successfully authenticated against the radius server. The traffic from the customer's probes (parent-proxies) is allowed to be passed without authentication as long as the destination is an allowed URL. All other traffic is denied and logged in the </var/log/squid/access.log> file.The following files set the criteria for the allowed trffic:

 - localnet.acl (/etc/squid/localnet.acl) - this file defines the resources that can use proxy server.
 - allowed-sites.acl (/etc/squid/allowed-sites.acl) - this file defines the URLs that are allowed through proxy service.
 - probes.acl - (/etc/squid/probes.acl) - this file defines the parent proxies. (customer probes)
 - regex.acl - (/etc/squid/regex.acl) - this file defines the URLs that are allowed through proxy service in the form of regular expressions.

## PARENT PROXY (customer probes)

The traffic to the customer sites is passed by the child proxy to the customer parent proxy. Parent proxy will forward the traffic as long as it is coming from the valid source (only child proxy is allowed) and going to the allowed URL. Parent proxies by default should allow the access only to the customer domain they are part of. 
The following files set the creteria for the allowed traffic:

- localnet.acl (/etc/squid/localnet.acl) - this file defines the resources that can use proxy server.
- allowed-sites.acl (/etc/squid/allowed-sites.acl) - this file defines the URLs that are allowed through proxy service.




