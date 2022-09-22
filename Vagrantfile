# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.provider "virtualbox" do |vb|  
    vb.memory = 1024 
    vb.cpus = 2
  end

  config.vm.define "db1" do |db|
    db.vm.hostname = "db1.local"
    db.vm.network "private_network", ip: "192.168.56.10"
    db.vm.provision "ansible", playbook: "mysql_provision.yml"

  end
  
  config.vm.define "web1" do |web|
    web.vm.hostname = "web1.local"
    web.vm.network "private_network", ip: "192.168.56.15"
    web.vm.network "forwarded_port", guest: 80, host: 28080 
    web.vm.provision "ansible", playbook: "wordpress_provision.yml"
  end

  config.vm.define "lb1" do |lb|
    lb.vm.hostname = "lb1.local"
    lb.vm.network "private_network", ip: "192.168.56.16"
    lb.vm.provider "virtualbox" do |lbvb|
      lbvb.memory = 512
    end  
  end

end
