# local-k8s-cluster-vagrant-ansible

Local kubernetes cluster with master and worker node setup using vagrant and ansible for local development and testing

## Prerequisites
- Ansible
- Minimum 8 GB of RAM (For default 3 VM instance with default configuration)
- Vagrant
- Virtualbox
- Minimum 40 GB of Disk space (For default 10 GB and 3 VM instance custom VM count and size needs different space)

## setup
Prior to running out vagrant file you need to install two vagrant plugin
- vagrant-disksize ( To increase disksize of vagrant box )
- vagrant-vbguest ( To install vbguest for guest machine )

## Running kubernetes cluster
After installing all requirements and setup, to run kubernetes cluster run command
```
git clone https://github.com/iamsuarvsharma/k8s-vagrant-virtualbox.git
cd k8s-vagrant-virtualbox
vagrant up
```
Which will run 3 VM instance with 1 master and 2  worker nodes.
No of nodes and some configuration can be easily modified by changing value in Vagrantfile
Some of variable are:
| Variable | Default value | Description |
|:--------:|:-------------:|:-----------:|
| N        | 2             | No of worker node |
| MASTER_MEMORY   | 2048   | RAM of master |
| MASTER_CPUS     | 2      | CPU of master |
| MASTER_DISK     | "10GB" | Disk size of master. Can be in MB, GB or TB |
| WORKER_MEMORY   | 1024   | RAM of worker |
| WORKER_CPUS     | 1      | CPU of Worker |
| WORKER_DISK     | "10GB" | Disk size of worker. Can be in MB, GB or TB |


## Accessing kubernetes cluster
For accessing kubernetes cluster you can ssh into k8s-master. To ssh into k8s-master run
```
vagrant ssh k8s-master
```
