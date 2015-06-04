# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "codemachine"
  config.vm.provision :shell, path: "./synced_folder/scripts/bootstrap.sh"
  config.vm.synced_folder 'synced_folder', '/home/vagrant/synced_folder', type: 'nfs' 

  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "100"]
    v.memory = 4096 
    v.customize ["modifyvm", :id,  "--natdnsproxy1", "off"]
    v.customize ["modifyvm", :id,  "--natdnshostresolver1", "off"]
    v.customize ["modifyvm", :id,  "--nictype1", "virtio"]
    v.customize ["modifyvm", :id,  "--nictype2", "virtio"]
  end

  config.ssh.forward_agent = true
  config.vm.network "private_network", type: "dhcp"

  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 3030, host: 3030
  config.vm.network "forwarded_port", guest: 4567, host: 4567
end
