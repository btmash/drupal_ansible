# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |cluster|
  cluster.vm.define :web1 do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network "private_network", ip: "10.0.0.2"
    config.vm.hostname = "web1"
    config.vbguest.auto_update = false
  end

  cluster.vm.define :db1 do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network "private_network", ip: "10.0.0.3"
    config.vm.hostname = "db1"
    config.vbguest.auto_update = false
  end

  cluster.vm.provision :ansible do |ansible|
    ansible.playbook = "install_python.yml"
    ansible.vault_password_file = "./vault_file"
    ansible.groups = {
      "db" => ["db1"],
      "web" => ["web1"],
    }
  end

  cluster.vm.provision :ansible do |ansible|
    ansible.playbook = "provision.yml"
    ansible.tags = "init"
    ansible.vault_password_file = "./vault_file"
    ansible.groups = {
      "db" => ["db1"],
      "web" => ["web1"],
    }
  end
end
