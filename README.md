iptables
========

Installs and configures iptables.

Requirements
------------

This role requires Ansible 1.4 or higher.

Role Variables
--------------

| Name                  | Default                                                                       | Description                                   |
|-----------------------|-------------------------------------------------------------------------------|-----------------------------------------------|
| iptables_icmp_enabled | true                                                                          | Enable/disable ICMP                           |
| iptables_rules        | [{protocol: tcp, source_addresses: 0.0.0.0/0, port: 22, comment: "OpenSSH" }] | Array of firewall rules represented as hashes |

Dependencies
------------

CentOS:
  - kbrebanov.selinux

Example Playbook
----------------

Install and configure iptables to allow ICMP and OpenSSH
```
- hosts: all
  roles:
    - { role: kbrebanov.iptables }
```

Install and configure iptables to disallow ICMP, allow OpenSSH and HTTP
```
- hosts: all
  roles:
    - { role: kbrebanov.iptables, iptables_icmp_enalbed: false, iptables_rules: [{protocol: tcp, source_addresses: 0.0.0.0/0, port: 22, comment: "OpenSSH"}, {protocol: tcp, source_addresses: 0.0.0.0/0, port: 80, comment: "HTTP"}] }
```

License
-------

BSD

Author Information
------------------

Kevin Brebanov
