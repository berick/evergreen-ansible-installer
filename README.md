# Evergreen / OpenSRF Ansible Installer

## Quick How-To

### Get the Installer

Clone and run the Ansible playbook using an Ubuntu login which has sudo
(but not as root).

```sh
sudo apt install -y git ansible
git clone --branch working/ubuntu-22.04-redis https://github.com/berick/evergreen-ansible-installer.git
cd evergreen-ansible-installer
```

### Install Evergreen with OpenSRF+Redis

The OpenSRF+Redis code currently lives in a working branch.

```sh
sudo ansible-playbook playbook.yml \
    -e using_redis=true \
    -e osrf_git_repository=git://git.evergreen-ils.org/working/OpenSRF.git \
    -e osrf_git_branch=collab/berick/lp2017941-opensrf-on-redis-v3
```

### Open the Browser Client

In Chrome/FF navigate to https://<HOSTNAME>/eg/staff/ and click 
through the SSL warning to access the staff client.

## Settings

Settings are stored in settings.yml.  There are a lot of options.  Please
review these values before installing.  Some items of note:

* load_sample_data: Test data is loaded into the database by default.

## File Structure

### playbook.yml 

Main playbook.  It organizes the tasks.

### settings.yml

Installation settings.  Modify as needed, override via -e var=val
ansible command line option, or store multiple overrides in a file
local_settings.yml and override via -e @local_settings.yml.

### \*/main.yml

Entry point for each collection of sub-tasks.

### extras

Optional packages and configuration not strictly required for OpenSRF 
and Evergreen.
