# -*- mode: ruby -*-
# vi: set ft=ruby :
IMAGE_NAME = "ubuntu/bionic64"
N = 1
MASTER_MEMORY = 2048
MASTER_CPUS = 2
MASTER_DISK = "5GB"
WORKER_MEMORY = 1024
WORKER_CPUS = 1
WORKER_DISK = "5GB"

Vagrant.configure("2") do |config|
    config.vagrant.plugins = ["vagrant-disksize", "vagrant-vbguest"]
    config.vm.box = IMAGE_NAME
    config.vm.define "k8s-master" do |master|
        master.vm.network :private_network, ip: "192.168.50.10"
        master.vm.hostname = "k8s-master"
        master.disksize.size = MASTER_DISK
        master.vm.provider "virtualbox" do |vb|
            vb.name = "k8s-master"
            vb.memory = MASTER_MEMORY
            vb.cpus = MASTER_CPUS
        end
        master.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "configure-master.yaml"
            ansible.extra_vars = {
                node_ip: "192.168.50.10",
            }
            ansible.verbose = true
        end
    end
    (1..N).each do |i|
        config.vm.define "worker-#{i}" do |worker|
            worker.vm.network :private_network, ip: "192.168.50.#{i + 10}"
            worker.vm.hostname = "worker-#{i}"
            worker.disksize.size = WORKER_DISK
            worker.vm.provider "virtualbox" do |vb|
                vb.name = "worker-#{i}"
                vb.memory = WORKER_MEMORY
                vb.cpus = WORKER_CPUS
            end
            worker.vm.provision "ansible_local" do |ansible|
                ansible.playbook = "configure-worker.yaml"
                ansible.extra_vars = {
                    node_ip: "192.168.50.#{i + 10}"
                }
                ansible.verbose = true
            end
        end
    end 
end
