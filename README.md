# Ansible firewall role

An ansible role that installs and configures a firewall with UFW.

The role includes the following tasks:
1. Install UFW.
2. Enable logging if it is required by the `firewall_enable_log` variable.
3. Allow SSH connections.
4. Allow connections specified by the `firewall_allowed_ports` variable.
5. Allow incoming access from IP addresses specified by the `firewall_allowed_hosts` variable.
6. Deny all other connections and enable firewall.

This role can be run under all versions of Ubuntu and Debian.

## Requirements

None

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
firewall_allowed_ports: []    # List of allowed ports
firewall_allowed_hosts: []    # List of allowed hosts
firewall_enable_log: True     # Enable/disable logging
```

The rest of the variables can be found at `vars/main.yml`:

```yaml
ansible_become: yes           # Activate privilege escalation
apt_cache_valid_time: 86400   # Cache update frequency in seconds
```

## Dependencies

None

## Example Playbook

The playbook example below includes a list of some allowed ports for the role:

```yaml
- hosts: all
  roles:
    - role: firewall
      firewall_allowed_ports:
       - http         # Allow all http connections
       - https        # Allow all https connections
       - 3000         # Allow all connections on port 3000
```

Use the corresponding variables to add ports and hosts to the lists of allowed values:

```yaml
firewall_allowed_ports:
  - 443
  - ftp
firewall_allowed_hosts:
  - '{{ groups["all"] | map("extract", hostvars, ["network_private_ip"]) | list }}'   # Allow connections from private IP addresses
  - '15.15.15.51'
```

> Note that each host should include `network_private_ip` variable to define which IP must be used for internal requests.

## License

Licensed under the [MIT License](https://opensource.org/licenses/MIT).
