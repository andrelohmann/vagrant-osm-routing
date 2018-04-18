# -*- mode: ruby -*-
# vi: set ft=ruby :

#require necessary plugins
required_plugins = %w( vagrant-hostmanager vagrant-vbguest )
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.include_offline = true

  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = "2"
  end

  config.vbguest.auto_update = true

  config.vm.network "private_network", ip: "192.168.123.123"
  config.vm.hostname = "routing.lokal"
  config.hostmanager.aliases = %w(api.routing.lokal)

  config.vm.provision "ansible_local" do |ansible|
    ansible.install = true
    ansible.install_mode = :pip
    ansible.version = "latest"
    ansible.playbook = "ansible/playbook.yml"
    ansible.galaxy_role_file = "ansible/requirements.yml"
  end
end
