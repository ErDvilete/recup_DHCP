# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # General

  config.vm.box = "debian/bookworm64"
  
  
  # DHCP server
  
  config.vm.define "dhcp" do |dhcp|
    
    dhcp.vm.hostname = "dhcp"

    dhcp.vm.network "private_network",
                    ip: "192.168.56.10"
                    
    
    dhcp.vm.network "private_network",
                    ip: "192.168.10.10",
                    virtualbox__intnet: "intnet1"
    
    dhcp.vm.network "private_network",
                    ip: "192.168.20.10",
                    virtualbox__intnet: "intnet2"
    
    dhcp.vm.provision "install", type: "shell",
                      inline: "apt-get install -y isc-dhcp-server"

    dhcp.vm.provision "config", type: "shell", inline: <<-SHELL
        apt-get update 
        apt-get upgrade -y
        cp -v  /vagrant/dhcpd.conf /etc/dhcp/
        cp -v /vagrant/isc-dhcp-server /etc/default/
        systemctl restart isc-dhcp-server
        
    SHELL
  end
  
  # -------DHCP client red 1--------
  
  config.vm.define "c1" do |c1|
    
    c1.vm.hostname = "PC1"
    
    c1.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet1"              
  end

  # Cliente 2

  config.vm.define "c2" do |c2|
    
    c2.vm.hostname = "PC2"
    
    c2.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet1"
  end

  # Cliente 3

  config.vm.define "c3" do |c3|
    
    c3.vm.hostname = "PC3"
    
    c3.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet1"
  end

  # -----Clientes DHCP intnet 2------

  config.vm.define "c4" do |c4|
    
    c4.vm.hostname = "PC4"
    
    c4.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet2"               
  end

  # Cliente 5

  config.vm.define "c5" do |c5|
    
    c5.vm.hostname = "PC5"
    
    c5.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet2"
  end

  # Cliente 6

  config.vm.define "c6" do |c6|
    
    c6.vm.hostname = "PC6"
    
    c6.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet2"
  end
end
  
