# Ansible Playbook 
This repository contains an Ansible playbook and inventory file to automate the installation and basic configuration of Fail2Ban on multiple Debian/Ubuntu servers. 

## `Contents fail2ban-setup.yaml` 
- `fail2ban-setup.yaml` - Ansible playbook to install and configure Fail2Ban ansiblehosts.yaml 
- `ansiblehosts.yaml` - Inventory file listing the servers to manage 

## Inventory File 
The `ansiblehosts.yaml` file contains your target servers and connection details. 

## Playbook Details 
The `fail2ban-setup.yaml` playbook: 
- Installs Fail2Ban via APT 
- Enables SSH protection against brute-force attacks 
- Configures basic settings: 
   - bantime: 3600 seconds (1 hour) 
   - findtime: 600 seconds (10 minutes) 
   - maxretry: 5 failed attempts Ensures Fail2Ban starts on boot 

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
