# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider :virtualbox do |v|
    v.name = "jenkins"
    v.memory = 1024
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.hostname = "jenkins"
  config.vm.network :private_network, ip: "192.168.1.10"

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :jenkins do |jenkins|
  end

  # Install python-simplejson before provisioning with Ansible
  # see https://github.com/plone/ansible-playbook/issues/82
  config.vm.provision "shell", inline: "apt-get update"
  config.vm.provision "shell", inline: "apt-get install -y python-simplejson"

  # Ansible provisioner
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
  end
end
