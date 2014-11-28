iptables
========

Installs and configures iptables firewall.

Requirements
------------

This role requires Ansible 1.4 or higher.

Role Variables
--------------

    # Allow ICMP packets (ping)
    iptables_icmp_enabled: True

    # OpenSSH rules
    iptables_ssh_source: 0.0.0.0/0
    iptables_ssh_port: 22
    iptables_ssh_comment: OpenSSH
    iptables_ssh_enabled: True

    # Zabbix agent rules
    iptables_zabbix_agent_source: 0.0.0.0/0
    iptables_zabbix_agent_port: 10050
    iptables_zabbix_agent_comment: Zabbix agent
    iptables_zabbix_agent_enabled: False

    # MySQL rules
    iptables_mysql_source: 0.0.0.0/0
    iptables_mysql_port: 3306
    iptables_mysql_comment: MySQL
    iptables_mysql_enabled: False

Dependencies
------------

Example Playbook
----------------

1) Install and configure iptables to allow ICMP and OpenSSH

    - hosts: all
      roles:
         - { role: iptables }

2) Install and configure iptables to block ICMP and allow OpenSSH

    - hosts: all
      roles:
         - { role: iptables, iptables_icmp_enabled: False }

3) Install and configure iptables to block ICMP, allow OpenSSH and MySQL

    - hosts: all
      roles:
         - { role: iptables, iptables_icmp_enabled: False, iptables_mysql_enabled: True}

License
-------

BSD

Author Information
------------------

Kevin Brebanov
