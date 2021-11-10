# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.define "ubuntu_k3s" do |ubuntu_k3s|

  ubuntu_k3s.vm.network 'private_network', ip: "192.168.33.10",  virtualbox__intnet: true

  ubuntu_k3s.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disabled: true
  # ssh master node
  ubuntu_k3s.vm.network "forwarded_port", guest: 22, host: 2000 # Master Node SSH
  # kubectl api
  ubuntu_k3s.vm.network "forwarded_port", guest: 6443, host: 6443
  ubuntu_k3s.vm.network "forwarded_port", guest: 8080, host: 8080 # API Access
  # jaeger
  ubuntu_k3s.vm.network "forwarded_port", guest: 16686, host: 16686 # Jaeger HTTP Access
  ubuntu_k3s.vm.network "forwarded_port", guest: 16687, host: 16687 # Jaeger CR Access

  ubuntu_k3s.vm.network "forwarded_port", guest: 32368 , host: 32368

  config.vm.provider "virtualbox" do |vb|
    vb.name = "Ubuntu k3s"
    vb.memory = "4096"
    vb.cpus = "4"
  end

   args = []
    config.vm.provision "k3s shell script", type: "shell",
        path: "scripts/provision.sh",
        args: args
    end

end

