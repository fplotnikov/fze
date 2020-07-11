# Install ansible requirements with ansible galaxy

# Install roles
ansible-galaxy role install -r requirements.yml
# Install collections
ansible-galaxy collection install -r requirements.yml


# Playbooks descriptions

* host-vpn.yml  - playbook to setup openvpn server
* host-zabbix.yml - playbook to install zabbix agent on server and register on Zabbix server
* host-prepare.yml - playbook to install useful toolset on server ( optional. Ubuntu/Debian )
