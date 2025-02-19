
=========

Requirements
------------

Any Debian or Ubuntu should do.

Role Variables
--------------

```
# List of networks with name and CIDR to allow access through the proxy
squid_networks:
  - { name: "usernet", cidr: "192.168.50.0/24" }

# Log file location for Squid proxy access logs
squid_logfile: "/var/log/squid/access.log"
```

Example Playbook
----------------

```
- hosts: localhost
  roles:
          - role: squidproxy
            vars:
                squid_networks:
                    - { name: "usernet", cidr: "192.168.50.0/24" }
                squid_logfile: "/var/log/squid/access.log"
```

License
-------

GPL-3.0

Author Information
------------------

Thorina Boenke (https://www.ait.ac.at)
