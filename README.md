"OpenVPN" Ansible Role
=========

Deploy simple OpenVPN server and generate clients configs.

Requirements
------------

Remotes:
- Based on Debian OS
- Internet connection

Inventory file:
- localhost must be present

WARNING
-------

All generated TLS-keys in easyrsa folder has no password.
Do not use this solution for critical systems.

Removing clients is not supported.

Tags
----

Use this tags for limit role functionality:
- "__ovpn-clients__" - generate the clients configs files. You can use that if you want to add new clients for your server (Existing configs will no be overwritten)
- "__ovpn-server__" - deploy and configure OpenVPN server

Default - run with __all__ tags.

Role Variables
--------------

```
# OpenVPN server configuration
# Your server url, port and protocol
openvpn_url: you-vpn-server.com
openvpn_port: 1194
openvpn_protocol: udp

# true if you want use the Uncomplicated Firewall
# if false you may need to use other firewall
openvpn_use_ufw: false

# DNS-servers
openvpn_dns:
- 1.1.1.1

# Clients of your Open VPN server
openvpn_clients:
- name: client0

# Server for you CA-server (May be the same as ovpn-server, but that is not safe!)
openvpn_ca_host: localhost # !!! Must be in inventory

# TLS configuration
# CA-storage location on CA server
openvpn_easy_rsa_path: ~/ovpn-easy-rsa

# Client's ovpn-configs location on localhost
openvpn_clients_path: ~/ovpn-clients

# Server's common name (CN)
openvpn_server_cn: ovpn-server

# Distinguished Name (DN) of your CA
openvpn_easyrsa_req_cn: OpenVPN
openvpn_easyrsa_req_country: RU
openvpn_easyrsa_req_province: Moscow
openvpn_easyrsa_req_city: Moscow City
openvpn_easyrsa_req_org: None
openvpn_easyrsa_req_email: no@email.net
openvpn_easyrsa_req_ou: Community
```

Dependencies
------------

None.

Example Playbook
----------------

```
- hosts: servers
  roles:
  - role: spector517.openvpn
```

Example Inventory
-----------------

```
[you-ovpn-server]
your-server.com

[you-ca-server]
your-ca-server.com

[local]
localhost ansible_connection=local
```

Usage
-----

- Download the client app from [here](https://openvpn.net/community-downloads/)
- Import the ovpn-config file in the client app
- Connect to OpenVPN server using client config

License
-------

MIT
