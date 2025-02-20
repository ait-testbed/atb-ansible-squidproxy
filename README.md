# Squidproxy Role

An Ansible role that installs and configures Squid as a proxy server. It allows you to define ACLs for specific networks and logs HTTP/HTTPS activity.

## Requirements


Any Debian or RedHat-based Linux.

## Role Variables


```yaml
# List of networks with name and CIDR to allow access through the proxy
squid_networks:
  - { name: "usernet", cidr: "192.168.50.0/24" }

# Log file location for Squid proxy access logs
squid_logfile: "/var/log/squid/access.log"
```
## Example Playbook

```yaml
---
- hosts: localhost
  become: true
  roles:
    - role: squidproxy
      vars:
        squid_networks:
          - { name: "usernet", cidr: "192.168.50.0/24" }
        squid_logfile: "/var/log/squid/access.log"
```


## License


GPL-3.0

## Author Information


Thorina Boenke (https://www.ait.ac.at)
