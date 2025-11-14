# Infra Hex

Are you planning to host mutliple experimental applications on self-managed Virtual Machines (VMs), Virtual Private Servers (VPSs), or On-Prem Servers (OPSs)?

This project can help you setup the following on your server:
- Install Docker
- Install Nginx as Proxy
- Add SSH users for each experimental application


# Usage Instructions

## Pre-requisites:

- Setup SSH access to the server you want to configure
- Install [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- Install sshpass (`sudo apt install sshpass`)
- Purchase a domain to configure SSL for the domain

## Clone the project

You can clone the project using

```bash
git clone git@github.com:Questra-Digital/experimentation-infra-manager-hex.git
cd experimentation-infra-manager-hex
```
## Set the inventory file
- Rename the `playbooks/inventory/.example.host.yml` file to `playbooks/inventory/host.yml`
- Change the ansible host and ansible user values as per your server root user
- Change the values of container registery url, username and password to allow login to all users

## Set the vars
- Rename the `playbooks/vars/users.yml.sample` file to `playbooks/vars/users.yml`
- Rename the `playbooks/vars/domains.yml.sample` file to `playbooks/vars/domains.yml`
- Change the values as per your needs

## Create SSH keys for all users
- Create SSH key pair for all users in `playbooks/vars/users.yml`
- Place the keys in path as specified in the same file i.e. `playbooks/vars/users.yml`

## Change the domain url

Change the domain and email according to your domain in the `playbooks/setup_ssl/tasks/main.yml`

## Run ansible project

You can configure the SSH password and then run the ansible command

```bash
 export ANSIBLE_PASSWORD=<your ssh password>
cd playbooks
ansible-playbook main.yml \
   --extra-vars "ansible_password=$ANSIBLE_PASSWORD"
```

# For Contributors

## Pre-requisites:

- Setup SSH access to the server you want to configure
- Install [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- Install sshpass (`sudo apt install sshpass`)
- Install [Vagrant](https://developer.hashicorp.com/vagrant/docs/installation)
- Install [Virtualbox](https://www.virtualbox.org/wiki/Downloads)

## Clone the project

You can clone the project using

```bash
git clone git@github.com:Questra-Digital/experimentation-infra-manager-hex.git
cd experimentation-infra-manager-hex
```

## Set the vars
- Rename the `playbooks/vars/users.yml.sample` file to `playbooks/vars/users.yml`
- Rename the `playbooks/vars/domains.yml.sample` file to `playbooks/vars/domains.yml`
- Change the values as per your needs

## Create SSH keys for all users
- Create SSH key pair for all users in `playbooks/vars/users.yml`
- Place the keys in path as specified in the same file i.e. `playbooks/vars/users.yml`

## Create a server and provision using ansible
You can start a virtual server for testing the ansible code
```bash
vagrant up --provision
```
Note: SSL configuration will not work. Need to yet find a way for testing in vm created locally through vagrant
