# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.hostmanager.enabled = false


  config.vm.define "jenkins" do |jenkins|
    jenkins.vm.provider :virtualbox do |v|
      v.name = "jenkins"
      v.memory = 1024
      v.cpus = 2
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end
    config.vm.hostname = "jenkins"
    jenkins.vm.network :private_network, ip: "192.168.1.10"
  end

  config.vm.define "app" do |app|
    app.vm.provider :virtualbox do |v|
      v.name = "app"
      v.memory = 512
      v.cpus = 1
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end
    config.vm.hostname = "app"
    app.vm.network :private_network, ip: "192.168.1.11"
  end

  config.vm.provision "shell" do |s|
    s.inline = "apt-get update"
    s.inline = "apt-get install -y python-simplejson"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
  end

  if Vagrant.has_plugin?("vagrant-hostmanager")
    config.vm.provision :hostmanager
  end
end
