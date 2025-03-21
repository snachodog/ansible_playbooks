# Ansible Playbook 
This repository contains an Ansible playbook and inventory file to automate the installation and basic configuration of Fail2Ban on multiple Debian/Ubuntu servers. 

## `Contents fail2ban-setup.yaml` 
— Ansible playbook to install and configure Fail2Ban ansiblehosts.yaml 
— Inventory file listing the servers to manage 

## Inventory File 
The ansiblehosts.yaml file contains your target servers and connection details. 
Example format: 
```
[webservers] 
192.168.1.219 ansible_user=steve ansible_ssh_private_key_file=/home/steve/.ssh/id_ed25519 ansible_become=true 
192.168.1.43 ansible_user=steve ansible_ssh_private_key_file=/home/steve/.ssh/id_ed25519 ansible_become=true 
192.168.1.51 ansible_user=steve ansible_ssh_private_key_file=/home/steve/.ssh/id_ed25519 ansible_become=true
```

## Playbook Details 
The `fail2ban-setup.yaml` playbook: 
`
- Installs Fail2Ban via APT 
- Enables SSH protection against brute-force attacks 
- Configures basic settings: 
   - bantime: 3600 seconds (1 hour) 
   - findtime: 600 seconds (10 minutes) 
   - maxretry: 5 failed attempts Ensures Fail2Ban starts on boot 
### Playbook snippet:

- name: Install and configure Fail2Ban on all servers hosts: all become: true vars: bantime: 3600 
findtime: 600 maxretry: 5 tasks: 
   - name: Install Fail2Ban apt: name: fail2ban state: present update_cache: yes 
   - name: Ensure Fail2Ban service is enabled and running service: name: fail2ban state: started enabled: true 
   - name: Create custom jail.local config copy: dest: /etc/fail2ban/jail.local content: | [DEFAULT] bantime = {{ bantime }} findtime = {{ findtime }} maxretry = {{ maxretry }} 
```
[sshd] 
enabled = true 
```
owner: root group: root mode: '0644' 
   - name: Restart Fail2Ban to apply config service: name: fail2ban state: restarted 
 
## Usage 
Run the playbook: 
`ansible-playbook -i ansiblehosts.yaml fail2ban-setup.yaml --ask-become-pass`

You'll be prompted once for your sudo password. 

## Requirements 
- Ansible installed on your control machine 
- SSH public key authentication set up between control machine and target servers 
- Target servers should be Debian/Ubuntu-based 

## Security Notice 
*Do NOT store private SSH keys or sensitive credentials in this repository.*
 This repo is designed to be safe for public use as long as private keys and secrets are excluded. 

## License
