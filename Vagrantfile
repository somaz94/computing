# -*- mode: ruby -*-
# vi: set ft=ruby :

NODE_COUNT=2

Vagrant.configure("2") do |config|
    config.vm.box = "centos/7"

    config.vm.define "master" do |master|
        master.vm.hostname = "master.cloud.org"
        master.vm.network "private_network", ip: "192.168.56.101"
        master.vm.network "forwarded_port", guest: 22, host:2222, id: "ssh"
        master.vm.provider "virutalbox" do |v|
            v.customize ["modifyvm", :id, "--name", "Master(vagrant)"]
            v.customize ["modifyvm", :id, "--cpus", "1"]
            v.customize ["modifyvm", :id, "--memory", "1024"]
        end    
    end

    NODE_COUNT.times do |i|
        node_id = "worker#{i+1}"
        ip_address = "192.168.56.10#{i+2}"
        config.vm.define "worker#{i+1}" do |node|
            node.vm.hostname = "#{node_id}.cloud.org"
            node.vm.network "private_network", ip: "#{ip_address}"
            node.vm.network "forwarded_port", guest: 22, host: "#{i+2223}", id: "ssh"
            node.vm.provider "virtualbox" do |v|
                v.customize ["modifyvm", :id, "--name", "Worker#{i+1}(vagrant)"]
                v.customize ["modifyvm", :id, "--cpus", "1"]
                v.customize ["modifyvm", :id, "--memory", "1024"]
            end
        end
    end     
end

