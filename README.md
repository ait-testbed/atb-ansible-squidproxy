# Ansible Role: Squid Proxy 

Installs and configures the Squid proxy server on Debian/Ubuntu and RHEL/CentOS/Fedora systems.

This role performs the following actions:

*   Installs the `squid` package using the appropriate package manager (`apt` or `yum`).
*   Deploys a configuration file (`/etc/squid/squid.conf`) based on a Jinja2 template (`templates/squid.conf.j2`).
*   Configures Access Control Lists (ACLs) based on the provided `squid_networks` variable to allow client access.
*   Sets the access log file location.
*   Restarts and enables the `squid` service using `systemd`.

## Requirements

*   **Target OS:** Debian/Ubuntu or RHEL/CentOS/Fedora based distributions.
*   **Root Access:** Requires `become: yes` as the role installs packages, manages configuration files in `/etc`, and controls system services.
*   **Systemd:** Assumes `systemd` is the init system for service management.
*   **Ansible Version:** 2.9 or higher recommended.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml` - *Note: Defaults should be defined there*):

| Variable        | Required | Default                             | Type                | Description                                                                               |
| --------------- | -------- | ----------------------------------- | ------------------- | ----------------------------------------------------------------------------------------- |
| `squid_networks`| Yes      | `[]`  | List of Dictionaries | A list of network definitions allowed access. Each dict needs `name` (ACL name) and `cidr`. |
| `squid_logfile` | No       | `"/var/log/squid/access.log"`       | String              | The full path to the Squid access log file specified in the configuration.                |

**Note:** You *must* define `squid_networks` with at least one network for clients to be able to use the proxy, unless your `squid.conf.j2` template has other permissive rules. It's recommended to provide a sensible default list in `defaults/main.yml` or explicitly set it when calling the role.

## Dependencies

None.

## Example Playbook

```yaml
---
- hosts: proxy_servers # Or specific host group
  become: yes
  vars:
    # Define the networks allowed to use this proxy
    squid_networks:
      - { name: "internal_lan", cidr: "192.168.1.0/24" }
      - { name: "vpn_clients", cidr: "10.8.0.0/24" }

    # Optionally override the default log file location
    # squid_logfile: "/data/logs/squid_access.log"

  roles:
    # Reference the role, adjust name/path as needed
    - ansible-role-squidproxy

## License

GPL-3.0

## Author Information

Thorina Boenke (https://www.ait.ac.at)
