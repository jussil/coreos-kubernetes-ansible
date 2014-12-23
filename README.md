# Kubernetes cluster on CoreOS with ansible

This whole stack is put together with roughly these sources:
https://github.com/jameskyle/ansible-kubernetes
https://github.com/eparis/kubernetes-ansible
https://github.com/GoogleCloudPlatform/kubernetes/tree/master/docs/getting-started-guides/coreos
https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-kubernetes-on-top-of-a-coreos-cluster

#Installation
##Requirements
- 2x (atleast) CoreOS nodes (Version: 5.22.2.0 (alpha) tested)
  - Private network between nodes
  - DigitalOcean hosted machines tested
  - If you want to have nodes somewhere else..
    - ansible/roles/kubernetes/templates are using COREOS_PRIVATE_IPV4 environment variable for setting correct IP
    - /etc/environment file has to contain following variables describing network
      - `COREOS_PRIVATE_IPV4=10.10.10.11`
      - `COREOS_PUBLIC_IPV4=100.100.100.101`
- Ansible installed locally
  `pip install ansible` / `brew install ansible`

##Steps
- Create cluster host config for ansible
  - Copy ansible/inventory/example.cluster into ansible/inventory/dev.cluster
  - There must be atleast one master and one minion (or many)
  - Set public IP of each node
  - Set master_private_ip to match private ip address on master node
- Run ansible playbooks (in ansible directory)
  - To setup python on CoreOS, ansible needs it:
    `ansible-playbook -i inventory/dev.cluster setup-python.yml`
  - Install kubernetes and other dependencies:
    `ansible-playbook -i inventory/dev.cluster setup-kubernetes.yml`
- Verify that cluster is up and running
  - SSH into master node
  - Check if fleet knows about nodes: `fleetctl list-machines`
  - Check if kubernetes knows about minions: `kubecfg list minions`

#TO-DO
#Deployments
#Kubernetes
##Application cluster
##kube-apiserver
##kube-controller-manager
##kube-proxy
##kube-register
##kube-scheduler
##kubelet
#Docker
##Application containers
#Storage
##Persistency
##Data management
#CoreOS
##Linux distribution
##etcd
##fleet
##flannel
