# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.disksize.size = '15GB'
  config.vm.provider "virtualbox" do |vb|  
    vb.memory = 1024 
    vb.cpus = 2
  end

  config.vm.define "db1" do |db|
    db.vm.hostname = "db1.local"
    db.vm.provision "ansible", playbook: "mysql_provision.yml"
    db.vm.network "private_network", ip: "192.168.56.10"
#    db.vm.provider "virtualbox" do |vb|
#      vb.memory = "1024"
  end
  
  config.vm.define "web1" do |web|
    web.vm.network "private_network", ip: "192.168.56.15"
    web.vm.network "forwarded_port", guest: 80, host: 28080 
  end

  config.vm.define "lb1" do |lb|
    lb.vm.network "private_network", ip: "192.168.56.16"
  end

end
