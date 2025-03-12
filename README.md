# server-bootstrap-playbook

**Ansible Infrastructure Automation**

This repository contains an Ansible playbook (site.yml) for managing multiple servers, updating packages, and provisioning services such as Fail2Ban, Jenkins, and system hardening.
Features

✅ Automated package updates across different Linux distributions

✅ Role-based deployment (Base system, Fail2Ban, Jenkins)

✅ Multi-distro support: RHEL, Debian, Arch, SUSE, and Alpine



**Project Structure:**

├── inventory/              # Inventory files (hosts, groups, variables)
│   ├── servers      # List of servers grouped by roles
│   ├── host_vars/          # Variables assigned to individual hosts
├── roles/                  # Role-based configurations
│   ├── base/               # System essentials and hardening
│   ├── fail2ban/           # Intrusion prevention configuration
│   ├── jenkins-server/     # Jenkins installation and setup
├── site.yml                # Main playbook that runs all roles
├── README.md               # Project documentation
└── ansible.cfg             # Ansible configuration file

**Pre-requisites:**

    Install Ansible (sudo apt install ansible on Ubuntu or dnf install ansible on RHEL)
    Ensure SSH access is enabled for Ansible

**Setup & Usage:**

Modify inventory/inventory.ini to include your target servers:

[prod]

server1.example.com

server2.example.com

[jenkins-server]

jenkins.example.com



Run the Playbook:
ansible-playbook site.yml



Check Configuration:
ansible all -i inventory/servers -m ping



**Playbook Breakdown** (site.yml)

The site.yml playbook automates system setup and security configurations.
Pre-Tasks: Updating Package Cache

Before applying roles, the playbook updates the package cache for different distributions:

    RHEL (CentOS, Rocky, AlmaLinux): dnf update_cache
    Debian (Ubuntu, Debian): apt update_cache
    SUSE: zypper update_cache
    Arch: pacman -Sy --noconfirm
    Alpine: apk update_cache

**Roles Assigned to Groups**

    prod group
        base: System updates, security configurations, SSH hardening
        fail2ban: Prevents brute-force attacks

    jenkins-server group
        jenkins-server: Installs and configures Jenkins for CI/CD


