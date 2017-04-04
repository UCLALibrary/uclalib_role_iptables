# UCLALib Ansible Role: IPTables [![Build Status](https://travis-ci.org/UCLALibrary/uclalib_role_iptables.svg?branch=master)](https://travis-ci.org/UCLALibrary/uclalib_role_iptables)

Configures iptables using the Library's template on RHEL servers

This role allows you to modify the default template by creating new input chain rules

## Variables

iptables_allowed_input_rules - list variables that defines the various input rules

- src_ip - defines the source ip address for the input rule
- dest_port - defines the destination port for the input rule (e.g. 80, 443, etc.)
- protocol - defines the protocol to use for this input rule (e.g. tcp, udp, icmp, etc.)

## Sample Variable Definition

```
iptables_allowed_input_rules:
  - src_ip: 0.0.0.0
    dest_port: 80
    protocol: tcp
  - src_ip: 10.0.0.1
    dest_port: 443
    protocol: tcp
  - src_ip: 10.0.0.2
    dest_port: 53
    protocol: udp
```
This role is suitable for including in a playbook for configuring a larger application.

Example:
```
- name: uclalib_app_playbook.yml
  sudo: true
  hosts: test
  vars:
    iptables_allowed_input_rules:
      - src_ip: 0.0.0.0/0
        dest_port: 80
        protocol: tcp

  roles:
    - { role: uclalib_role_application}
    - { role: uclalib_role_iptables }
```

> License
> -------
>
> BSD 3-Clause