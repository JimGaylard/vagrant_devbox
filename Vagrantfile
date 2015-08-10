# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  HOME = ENV['HOME']


  config.vm.box = "trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.hostname = "vagrant"
  config.vm.box_download_checksum_type = "md5"
  config.vm.box_download_checksum = "1b839c754865f5d8998b1ac7a0edde93"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    vb.name = "devbox"
    vb.memory = 3072
    vb.cpus = 2
  end

  config.vm.network "private_network", ip: "192.168.34.25"
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
