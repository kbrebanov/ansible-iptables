iptables
========

[![Build Status](https://travis-ci.org/kbrebanov/ansible-iptables.svg?branch=master)](https://travis-ci.org/kbrebanov/ansible-iptables)

Installs and configures iptables.

Requirements
------------

This role requires Ansible 1.9 or higher.

Role Variables
--------------

| Name                             | Default                                                                               | Description                                 |
|:---------------------------------|:--------------------------------------------------------------------------------------|:--------------------------------------------|
| iptables_filter_input_policy     | drop                                                                                  | IPv4 default filter input policy            |
| iptables_filter_forward_policy   | drop                                                                                  | IPv4 default filter forward policy          |
| iptables_filter_output_policy    | accept                                                                                | IPv4 default filter output policy           |
| iptables_filter_rules            | [{protocol: tcp, source_address: 0.0.0.0/0, destination_port: 22, comment: OpenSSH }] | Array of filter rules represented as hashes |
| iptables_nat_prerouting_policy   | accept                                                                                | IPv4 default nat prerouting policy          |
| iptables_nat_input_policy        | accept                                                                                | IPv4 default nat input policy               |
| iptables_nat_output_policy       | accept                                                                                | IPv4 default nat output policy              |
| iptables_nat_postrouting_policy  | accept                                                                                | IPv4 default nat postrouting policy         |
| iptables_nat_rules               | []                                                                                    | Array of nat rules represented as hashes    |
| iptables6_filter_input_policy    | drop                                                                                  | IPv6 default filter input policy            |
| iptables6_filter_forward_policy  | drop                                                                                  | IPv6 default filter forward policy          |
| iptables6_filter_output_policy   | accept                                                                                | IPv6 default filter output policy           |
| iptables6_nat_prerouting_policy  | accept                                                                                | IPv6 default nat prerouting policy          |
| iptables6_nat_input_policy       | accept                                                                                | IPv6 default nat input policy               |
| iptables6_nat_output_policy      | accept                                                                                | IPv6 default nat output policy              |
| iptables6_nat_postrouting_policy | accept                                                                                | IPv6 default nat postrouting policy         |

Dependencies
------------

None

Example Playbook
----------------

Install and configure iptables to allow ICMP and OpenSSH
```yaml
- hosts: all
  roles:
    - kbrebanov.iptables
```

Install and configure iptables to disallow ICMP, allow OpenSSH and HTTP
```yaml
- hosts: all
  vars:
    iptables_filter_rules:
      - chain: input
        protocol: tcp
        source_address: 0.0.0.0/0
        port: 22
        comment: OpenSSH
      - chain: input
        protocol: tcp
        source_address: 0.0.0.0/0
        port: 80
        comment: HTTP
  roles:
    - kbrebanov.iptables
```

Install and configure iptables with a port forward rule for HTTP
```yaml
- hosts: all
  vars:
    iptables_filter_rules:
      - chain: input
        protocol: tcp
        source_address: 0.0.0.0/0
        destination_port: 80
        comment: HTTP
    iptables_nat_rules:
      - chain: prerouting
        protocol: tcp
        destination_port: 80
        to_destination: 192.168.1.54
        to_port: 8080
  roles:
    - kbrebanov.iptables
```

License
-------

BSD

Author Information
------------------

Kevin Brebanov
