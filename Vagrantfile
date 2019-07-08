# -*- mode: ruby -*-
# vi: set ft=ruby :

# https://docs.vagrantup.com.
Vagrant.configure("2") do |config|
  config.vm.box = "bento/debian-9.5"

  config.ssh.forward_agent = true

  # Install Ansible
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yaml"
    ansible.install_mode = "pip"
  end
end
