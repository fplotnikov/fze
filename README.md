# Install ansible requirements with ansible galaxy

### Install roles
`ansible-galaxy role install -r requirements.yml`
### Install collections
`ansible-galaxy collection install -r requirements.yml`


# Playbooks descriptions

* host-vpn.yml  - playbook to setup openvpn server
* host-zabbix.yml - playbook to install zabbix agent on server and register on Zabbix server
* host-prepare.yml - playbook to install useful toolset on server ( optional. Ubuntu/Debian )

# To setup server proceed with following procedure:
1. Pull repo
2. Prepare environment:
    2.1 Add servers in hosts file
    2.2 Prepare "vpn" file in group_vars folder
3. Run ansible playbook and specify environment. Example: `ansible-playbook --private-key some_key.pem -u ubuntu -b -i environments/dev/hosts host-vpn.yml`

Order in which you run setup is not important. 

# Variables description

Fill certificates details here:

>    easyrsa_conf_req_country: UA
>    easyrsa_conf_req_province: "Lviv"
>    easyrsa_conf_req_city: "Lviv"
>    easyrsa_conf_req_org: "Upwork DEV"
>    easyrsa_conf_req_email: "info@upwork.localdomain"
>    easyrsa_conf_req_ou: "Upwork IT"

Put server name here. Will be used for server certificate creation.
>easyrsa_servers:
>    - name: server

Client names certificates which will be generated
>easyrsa_clients:
>    - name: client1
>    - name: client2


OpenVPN section:

Host IP to bind OpenVPN and firewall management
> openvpn_open_firewall: true
> openvpn_host: "{{ ansible_default_ipv4.address }}"

Port and protocol to bind OpenVPN
> openvpn_port: 443
> openvpn_proto: tcp

General OpenVPN settings . Read official doc for details. 
> openvpn_server_options: [ 
>     'push "redirect-gateway def1"',
>     'push "remote-gateway {{ ansible_default_ipv4.address }}"',
>     'push "dhcp-option dns 8.8.8.8"'
> ]
> openvpn_dev: tun
> openvpn_use_pam: no
> openvpn_unified_client_profiles: yes


# zabbix part
zabbix_server: 192.168.33.30
zabbix_api_user: Admin
zabbix_api_pass: zabbix
zabbix_host_groups: "Linux Servers"
zabbix_link_templates: "Template OS Linux"
zabbix_install_pip_packages: false
