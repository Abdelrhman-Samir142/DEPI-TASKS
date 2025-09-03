<img width="1917" height="1032" alt="Screenshot 2025-09-03 194944" src="https://github.com/user-attachments/assets/1fec972c-02c3-4a8f-bcb8-a4d2a811c788" /># Ansible SSH Key-Based Authentication Setup

This guide walks you through setting up SSH key-based authentication for Ansible on a local system using managed users. This is particularly useful for testing Ansible playbooks locally or setting up a development environment.

## Overview

This setup creates two managed users (`node1` and `node2`) on your local system and configures SSH key-based authentication so Ansible can manage them without password prompts.

## Prerequisites

- Linux system with sudo privileges
- Ansible installed
- SSH server running on localhost

## Step-by-Step Setup

### 1. Create Managed Users

```bash
sudo adduser node1
sudo adduser node2
```

This creates two system users that will act as your managed nodes.

### 2. Generate SSH Key Pairs

```bash
ssh-keygen -t rsa -f ~/.ssh/id_rsa_node1
ssh-keygen -t rsa -f ~/.ssh/id_rsa_node2
```

- Creates RSA key pairs for each node
- Private keys: `~/.ssh/id_rsa_node1` and `~/.ssh/id_rsa_node2`
- Public keys: `~/.ssh/id_rsa_node1.pub` and `~/.ssh/id_rsa_node2.pub`
- Press Enter when prompted for passphrase (leave empty for automation)

### 3. Configure SSH Access for node1

```bash
sudo mkdir -p /home/node1/.ssh
sudo cp ~/.ssh/id_rsa_node1.pub /home/node1/.ssh/authorized_keys
sudo chown -R node1:node1 /home/node1/.ssh
sudo chmod 700 /home/node1/.ssh
sudo chmod 600 /home/node1/.ssh/authorized_keys
```

### 4. Configure SSH Access for node2

```bash
sudo mkdir -p /home/node2/.ssh
sudo cp ~/.ssh/id_rsa_node2.pub /home/node2/.ssh/authorized_keys
sudo chown -R node2:node2 /home/node2/.ssh
sudo chmod 700 /home/node2/.ssh
sudo chmod 600 /home/node2/.ssh/authorized_keys
```

**Important:** The SSH directory permissions are critical for security:
- `.ssh` directory: `700` (owner read/write/execute only)
- `authorized_keys` file: `600` (owner read/write only)

### 5. Test SSH Connectivity

```bash
ssh -i ~/.ssh/id_rsa_node1 node1@localhost
ssh -i ~/.ssh/id_rsa_node2 node2@localhost
```

These commands should connect without asking for a password. Type `exit` to return to your original shell.

### 6. Create Ansible Inventory

```bash
cat > ~/inventory.ini <<EOL
[nodes]
node1 ansible_host=127.0.0.1 ansible_user=node1 ansible_ssh_private_key_file=/home/samir/.ssh/id_rsa_node1
node2 ansible_host=127.0.0.1 ansible_user=node2 ansible_ssh_private_key_file=/home/samir/.ssh/id_rsa_node2
EOL
```

**Note:** Replace `/home/samir/` with your actual home directory path (use `echo $HOME` to find it).

### 7. Test Ansible Connectivity

```bash
ansible all -i ~/inventory.ini -m ping
```

Expected output:
```
node1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
node2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}


