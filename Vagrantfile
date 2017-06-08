# -*- mode: ruby -*-
# vi: set ft=ruby :

box = "ubuntu/xenial64"
boxName = "ansible-snp"

boxAnsible = "./ansible/"
boxAnsibleConfig = "ansible.cfg"
boxPlaybook = "vagrant.yaml"
boxInventory = "inventory"

ENV['ANSIBLE_ROLES_PATH'] = boxAnsible+"roles"

Vagrant.configure("2") do |config|

  config.vm.box = box

  config.vm.define boxName do |xenialtest|
    xenialtest.vm.hostname = boxName
    xenialtest.vm.network "private_network", type: "dhcp"
    xenialtest.vm.provider :virtualbox do |v|
      v.name = boxName
    end
  end

  # Install python2.7 to make Ansible work
  config.vm.provision "shell", inline: <<-SHELL
    if [[ -z $(which python) ]]; then
        apt update && apt install -y python
    fi
  SHELL

  config.vm.provision :ansible do |ansible|
    ansible.config_file = boxAnsible+boxAnsibleConfig
    ansible.inventory_path = boxAnsible+boxInventory
    ansible.playbook = boxAnsible+boxPlaybook
  end

end