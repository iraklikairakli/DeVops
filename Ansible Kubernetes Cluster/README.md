# Ansible Kubernetes 
## How to run Kubernetes with ansible

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)
## HOST ( host file )
```sh
[masters]
master-1 ansible_host=10.0.76.201 ansible_user=root
master-2 ansible_host=10.0.76.202 ansible_user=root
master-3 ansible_host=10.0.76.203 ansible_user=root
master-4 ansible_host=10.0.76.204 ansible_user=root
[masters-init]
master-2 ansible_host=10.0.76.202 ansible_user=root
master-3 ansible_host=10.0.76.203 ansible_user=root
master-4 ansible_host=10.0.76.204 ansible_user=root
[workers]
worker-1 ansible_host=10.0.76.205 ansible_user=root
worker-2 ansible_host=10.0.76.206 ansible_user=root
worker-3 ansible_host=10.0.76.207 ansible_user=root
[lb]
lb-1 ansible_host=10.0.76.208 ansible_user=root
lb-2 ansible_host=10.0.76.209 ansible_user=root
```

## How to run
```sh
ansible-playbook -i hosts my_playbook.yaml
time ansible-playbook -i hosts my_playbook.yaml #see time
```
