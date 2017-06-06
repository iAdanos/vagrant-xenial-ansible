# -*- mode: ruby -*-
# vi: set ft=ruby :

# Deafult config
defaultBox = "debian/jessie64"
defaultBoxUser = "vagrant"
defaultBoxName = "ansible-snp"
defaultAnsible = "ansible/"
defaultPlaybook = "vagrant.yaml"

# Apply user config
box = ENV['BOX'] || defaultBox
boxName = ENV['BOX_NAME'] || defaultBoxName
boxUser = ENV['BOX_USER'] || defaultBoxUser
boxAnsible = ENV['BOX_ANSIBLE'] || defaultAnsible
boxPlaybook = ENV['BOX_PLAYBOOK'] || defaultPlaybook

# Setup environement
ENV['ANSIBLE_ROLES_PATH'] = boxAnsible+"roles"

# Setup user name for Ubuntu Linux
if ENV['OS'] == "Ubuntu" || ENV['BOX'] == "ubuntu/xenial64"
  box = "ubuntu/xenial64"
  boxUser = "ubuntu"
end

# Vagrant box configuration itself
Vagrant.configure("2") do |config|
 
  config.vm.box = box

  config.vm.define boxName do |vagrantvm|
    vagrantvm.vm.hostname = boxName+".vagrant"
    vagrantvm.vm.network "private_network", type: "dhcp"
    vagrantvm.vm.provider :virtualbox do |v|
      v.name = boxName
    end
  end

  if ENV['OS'] == "Ubuntu" || ENV['BOX'] == "ubuntu/xenial64"
    config.vm.provision "shell", inline: <<-SHELL
    apt update
    apt install -y python
  SHELL
  end


  config.vm.provision :ansible do |ansible|
    ansible.playbook = boxAnsible+"/"+boxPlaybook
    ansible.sudo = true
    ansible.groups = {
      "vagrant" => [boxName],
    }
    ansible.extra_vars = {
      ansible_ssh_user: boxUser,
      hbase_standalone:   true,
    }
  end
  
#  config.vm.provision :ansible do |ansible|
#    ansible.playbook = "prepare.yml"
#    ansible.sudo = true
#    ansible.groups = {
#      "vagrant" => ["ansible-snp"],
#    }
#    ansible.extra_vars = {
#      ansible_ssh_user: 'vagrant',
#      hbase_standalone:   true,
#    }
#  end


end
