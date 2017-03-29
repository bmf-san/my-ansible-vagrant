# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Box name
  config.vm.box = "centos7.3"

  # Time setting
  config.vm.provider :virtualbox do |vb|
    vb.customize ["setextradata", :id, "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled", 0]
  end

  # Synced Folder
  config.vm.synced_folder "/Users/takeuchikenta/localdev", "/var/www/html",
    :owner => "nginx",
    :group => "nginx",
    :mount_options => ["dmode=775,fmode=664"]

  # Provisioning
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/site.yml"
    ansible.inventory_path = "ansible/host"
    ansible.limit = 'all'
  end

  # Port
  #config.vm.network "forwarded_port", guest: 80, host: 8080

  # Network - Host Updator
  config.vm.network :private_network, ip: "192.168.33.111"
  config.vm.hostname = "localdev"
  config.hostsupdater.aliases = ["localdev-alias"]
end
