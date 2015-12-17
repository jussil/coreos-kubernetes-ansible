# Kubernetes cluster on CoreOS with ansible

# Requirements
- Ansible
- Vagrant + Virtualbox / VMWare

# Installation
```
#!shell
ansible-galaxy install -r ansible/requirements.yml -p ansible/roles
cd vagrant
vagrant up
```

If for some reason there is some sort of errors, try halting and upping:

- ```vagrant halt && vagrant up```

Or if services are not running, try provisioning:

-```vagrant provision```
