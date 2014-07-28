# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  HOME = ENV['HOME']

  config.vm.box = "ubuntu-14.04-cloud-image"
  config.vm.hostname = "vagrant"

  config.vm.network "private_network", ip: "192.168.34.20"
  config.ssh.forward_agent = true

  config.vm.synced_folder HOME, "/host_home"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision/main.yml"
    ansible.inventory_path = "ansible_hosts"
    ansible.limit = "all"
    ansible.verbose = "v"
  end

  config.vm.provider "virtualbox" do |vb|
    vb.name = "devbox"
    vb.memory = 4096
    vb.cpus = 4
    #vb.customize ["modifyvm", :id, "--memory", "4096"]
  end
end
