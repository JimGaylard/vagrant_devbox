# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  HOME = ENV['HOME']

  #config.vbguest.auto_update = false

  config.vm.box = "xenial-server-cloudimg-amd64-vagrant-disk1"
  config.vm.box_url = "https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-vagrant.box"

  config.vm.hostname = "vagrant"

  config.ssh.username = 'ubuntu'

  config.vm.provider :virtualbox do |vb|
    # Use this this to debug startup problems if necessary.
    # vb.gui = true
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    vb.name = "dev"
    vb.memory = 3072
    vb.cpus = 2
    v.customize [
      "storagectl", :id,
      "--name", "SATA Controller",
      "--hostiocache", "on"
    ]
  end

  config.vm.network "private_network", ip: "192.168.34.25"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 12345, host: 12345
  config.ssh.forward_agent = true

  config.nfs.map_uid = Process.uid
  config.nfs.map_gid = Process.gid

  config.vm.synced_folder HOME, "/host_home",
    type: 'nfs',
    mount_options: [
      'vers=3',
      'udp',
      'nolock'
    ]

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision/main.yml"
    ansible.inventory_path = "ansible_hosts"
    ansible.limit = "all"
    ansible.verbose = "v"
  end
end
