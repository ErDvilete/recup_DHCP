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
                    ip: "192.168.10.1",
                    virtualbox__intnet: "intnet1" #Este es el primer grupo de red
    
    dhcp.vm.network "private_network",
                    ip: "192.168.20.1",
                    virtualbox__intnet: "intnet2" #Este es el segundo grupo de red
    
    dhcp.vm.provision "install", type: "shell",
                      inline: <<-SHELL
                      apt-get update
                      apt-get upgrade -y
                      apt-get install isc-dhcp-server -y
                      SHELL

    dhcp.vm.provision "config", type: "shell", inline: <<-SHELL
        cp -v  /vagrant/dhcpd.conf /etc/dhcp/ #Copiamos a dentro del sistema el archivo de configuración
        cp -v /vagrant/isc-dhcp-server /etc/default/ #Guardamos el archivo de configuración del servidor DHCP
        systemctl restart isc-dhcp-server
        
    SHELL
  end
  
  # -------DHCP client red 1--------
  
  config.vm.define "c1" do |c1|
    
    c1.vm.hostname = "PC-9"
    
    c1.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet1"
  end

  # Cliente 2

  config.vm.define "c2" do |c2|
    
    c2.vm.hostname = "PC-10"
    
    c2.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet1",
                  ip: "192.168.10.101",
                  mac: "001AA0E8C239"
  end

  # Cliente 3

  config.vm.define "c3" do |c3|
    
    c3.vm.hostname = "PC-11"
    
    c3.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet1",
                  ip: "192.168.10.102",
                  mac: "001AA0E6094A"
  end

  # -----Clientes DHCP intnet 2------

  config.vm.define "c4" do |c4|
    
    c4.vm.hostname = "PC-12"
    
    c4.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet2"
  end

  # Cliente 5

  config.vm.define "c5" do |c5|
    
    c5.vm.hostname = "PC-13"
    
    c5.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet2",
                  ip: "192.168.20.101",
                  mac: "001AA0E5F5D2"
  end

  # Cliente 6

  config.vm.define "c6" do |c6|
    
    c6.vm.hostname = "PC-14"
    
    c6.vm.network "private_network",
                  type: "dhcp",
                  virtualbox__intnet: "intnet2",
                  ip: "192.168.20.102",
                  mac: "001AA0E906CF" #Ponemos las MAC que se nos da en el pdf de la practica
  end
end
