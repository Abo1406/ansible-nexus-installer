# Ansible Nexus Repository Installer

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=flat&logo=ansible&logoColor=white)

Automated deployment of Sonatype Nexus Repository Manager using Ansible. This playbook installs prerequisites, configures Nexus, creates a dedicated system user, and starts the service.

## Features

- Installs Java 8 and essential networking tools
- Downloads and extracts the latest Nexus Repository Manager
- Configures dedicated `nexus` system user with proper permissions
- Auto-starts Nexus service on deployment
- Service verification with process/port checks

## Prerequisites

- **Control Machine**: Ansible 2.9+
- **Target Host**: Ubuntu/Debian (tested on 20.04/22.04)
- **Permissions**: SSH access with sudo privileges to target host

## Usage

### 1. Clone Repository
```bash
git clone https://github.com/your_username/ansible-nexus-installer.git
cd ansible-nexus-installer
```
### 2. Configure Inventory
Edit inventory.ini:
```bash
[nexus_server]
192.168.1.100  # Replace with your server IP

[nexus_server:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/your_key.pem
```
### 3. Run Playbook
```bash
ansible-playbook -i inventory.ini deploy_nexus.yml
```

## Playbook Workflow
1. Install Dependencies:
   * Updates dnf cache
   * Installs OpenJDK 8 and net-tools
2. Deploy Nexus:
   * Downloads latest Nexus binary
   * Extracts to /opt/nexus
   * Configures directory permissions
3. Configure Service:
   * Creates nexus system user
   * Sets run_as_user in config
   * Starts Nexus service
4. Verification:
   * Checks running processes
   * Validates port 8081 accessibility
## Post-Installation
   * Access Nexus: http://<SERVER_IP>:8081
   * Admin password: /opt/sonatype-work/admin.password
   * Default credentials: admin / (password from file)
## License
MIT License - see LICENSE for details.
