# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "trusty64"

  config.vm.synced_folder "~/workspaces/osmlab/osm-slackbot.git", "/home/vagrant/osm-slackbot.git"

  config.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.cpus = 2
      vb.memory = 4096
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant.yml"
    ansible.host_key_checking = false
    ansible.verbose = "v"
    ansible.raw_arguments = [
      "--extra-vars=@extra_vars/vagrant.yml",
      "--extra-vars=@secret.yml"
    ]
  end

end
