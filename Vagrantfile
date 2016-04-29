# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = false
  config.vm.network "forwarded_port", guest: 22, host: 2232
  config.vm.network "private_network", ip: "192.169.50.4",
  virtualbox__intnet: true
  config.vm.hostname = "dpn7os"
  config.ssh.username = "vagrant"
  config.ssh.password = "vagrant"
  config.ssh.port = 2222

  config.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = "256"
      vb.cpus = "1"
  end

  #config.vm.synced_folder '.', '/home/vagrant/sync', type: "smb", mount_options: ["vers=3.02","mfsymlinks"]
  config.vm.synced_folder '.', '/home/vagrant/sync', :disabled => true

  config.vm.provision "shell", 
    inline: "echo Hello, World"

  config.vm.provision "file", source: "provisioning/playbook.yml", destination: "/home/vagrant/playbook.yml"


  config.vm.provision "ansible_local" do |ansible|
     ansible.install        = true
     ansible.provisioning_path = "/home/vagrant"
     ansible.playbook = "/home/vagrant/playbook.yml"
  end


end


