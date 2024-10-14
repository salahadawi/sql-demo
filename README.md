# MySQL Demo Automation with Ansible

  

This repository contains a set of Ansible playbooks designed to manage a MySQL database inside an Ubuntu Docker container. The functionality includes initializing the MySQL server, populating it with dummy data, backing it up, and restoring it from a backup.
  

## Prerequisites

  

#### Docker: 
Make sure Docker is installed on your machine. The setup uses a Docker container as the Ansible host and the MySQL server.

#### Python 3:
The Docker container should have Python 3 installed to execute the Ansible playbooks.


## Setting Up the Environment

  

### Run Ubuntu Docker Container

First, you’ll need to start an Ubuntu container. You can start the container using:

  
```bash
docker run --name sql-demo -d -it ubuntu
```
  

Once the container is running, you can access it like this:

  
```bash
docker exec -it sqldemo bash
```
  

  

### Install Python3 in the Container

After accessing the container, install Python3

  
```bash
apt install update && apt install -y python3
```

Now you’re ready to run the playbooks from your host machine.

  ## Running Ansible Playbooks

### sqldemo_initialize.yaml
This playbook installs and configures the MySQL server inside the Docker container and sets up the root user with a password.

```bash
ansible-playbook -i inventory.ini sqldemo_initialize.yaml
```
  

### sqldemo_populate.yaml

This playbook creates the sqldemo database and a users table with dummy data. It performs the following tasks:

```bash
ansible-playbook -i inventory.ini sqldemo_populate.yaml
```
  

### sqldemo_backup.yaml

This playbook performs a backup of the MySQL sqldemo database and fetches a copy of the backup to the local machine.
```bash
ansible-playbook -i inventory.ini sqldemo_backup.yaml
```

### sqldemo_drop.yaml

This playbook drops the sqldemo database.
```bash
ansible-playbook -i inventory.ini sqldemo_drop.yaml
```
  
### sqldemo_restore.yaml

This playbook restores the MySQL sqldemo database from a backup file. It:
```bash
ansible-playbook -i inventory.ini sqldemo_restore.yaml --e "backup_file=/remote_path/to/backup.sql"
```
