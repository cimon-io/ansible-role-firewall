Firewall role
=========

An Ansible Role that configures UFW

Requirements
----------------

None.

Role Variables
----------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

```
allowed_ports: []
```

List of allowed ports.

Dependencies
----------------

None.

Example Playbook
----------------

Example:

    - hosts: all
      roles:
         - role: firewall
           allowed_ports:
             - http
             - https
             - 3000

Also each host should define `specified_ip` variable to define which IP should be used for internal requests.

License
-------

MIT

