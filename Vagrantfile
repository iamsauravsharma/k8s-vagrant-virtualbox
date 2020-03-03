# -*- mode: ruby -*-
# vi: set ft=ruby :
IMAGE_NAME = "ubuntu/bionic64"
N = 2
MASTER_MEMORY = 2048
MASTER_CPUS = 2
MASTER_DISK = "10GB"
NODE_MEMORY = 1024
NODE_CPUS = 1
NODE_DISK = "10GB"

Vagrant.configure("2") do |config|
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
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "configure-master.yaml"
            ansible.extra_vars = {
                node_ip: "192.168.50.10",
            }
            ansible.verbose = true
        end
    end
    (1..N).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.network :private_network, ip: "192.168.60.#{i + 60}"
            node.vm.hostname = "node-#{i}"
            node.disksize.size = NODE_DISK
            node.vm.provider "virtualbox" do |vb|
                vb.name = "node-#{i}"
                vb.memory = NODE_MEMORY
                vb.cpus = NODE_CPUS
            end
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "configure-node.yaml"
                ansible.extra_vars = {
                    node_ip: "192.168.60.#{i + 60}"
                }
                ansible.verbose = true
            end
        end
    end 
end
