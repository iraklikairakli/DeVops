# Ansible Kubernetes 
## How to run Kubernetes with ansible

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

1. Change Host file ( add worker and node ip )
2. Create Ansible play-book
3. Run Ansible play-book
4. Init Kubernetes Cluster
5. Join Worker and Master
6. Install Calico

## 1. HOST ( host file )
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

## 3 .How to run ansible play-book
```sh
ansible-playbook -i hosts my_playbook.yaml
time ansible-playbook -i hosts my_playbook.yaml #see time
```
## 4. Init Kubernetes Cluster 
```sh
kubeadm init --control-plane-endpoint="virtual-ip:6443" --upload-certs --apiserver-advertise-address=master-1-ip --pod-network-cidr=192.168.0.0/16
```
## 5. After init cluster you see join command for worker and master 
###### master


```sh
kubeadm join virtual-ip:6443 --token 6du845.pbgmx0wcfptcm5wk \
>         --discovery-token-ca-cert-hash sha256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx \
>         --control-plane --certificate-key xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
###### worker
```sh
kubeadm join virtual-ip:6443 --token 6du845.pbgmx0wcfptcm5wk \
>         --discovery-token-ca-cert-hash xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```


## 6.Install/Deploy Calico
```sh
kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml 
kubectl create -f https://docs.projectcalico.org/manifests/custom-resources.yaml
```
