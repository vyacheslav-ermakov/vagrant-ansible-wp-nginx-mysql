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
    db.vm.network "private_network", ip: "192.168.56.15"
    db.vm.provision "ansible", playbook: "./provision/mysql_provision.yml"
  end
  
  config.vm.define "web1_wp" do |web1|
    web1.vm.hostname = "web1.local"
    web1.vm.network "private_network", ip: "192.168.56.10" 
    web1.vm.provision "ansible", playbook: "./provision/wordpress_provision.yml"
  end

  config.vm.define "web2_wp" do |web2|
    web2.vm.hostname = "web2.local"
    web2.vm.network "private_network", ip: "192.168.56.11"
    # temp
    web2.vm.network "forwarded_port", guest: 80, host: 38080
    web2.vm.provision "ansible", playbook: "./provision/wordpress_provision.yml"
  end

  config.vm.define "lb1" do |lb|
    lb.vm.hostname = "lb1.local"
    lb.vm.network "private_network", ip: "192.168.56.16"
    lb.vm.provision "ansible", playbook: "./provision/nginx_lb_provision.yml"
    lb.vm.provider "virtualbox" do |lbvb|
      lbvb.memory = 512
    end  
  end

end
