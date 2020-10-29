# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"
  config.env.enable

  config.vm.network "private_network", ip: "192.168.29.107"
  config.vm.network "forwarded_port", guest: 8111, host: 8111

  config.hostsupdater.aliases = [
    "teamcity.local",
  ]

  config.vm.provider "virtualbox" do |v|
    v.name = 'teamcity'
    v.memory = 3072
    v.cpus = 2
  end

  config.vm.provision "shell", inline: $set_environment_variables, run: "always"

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provisioning/main.yml"
    # ansible.tags = "aws_cli"
  end
end

$set_environment_variables = "echo 'source /vagrant/.env' > /etc/profile.d/sa-environment.sh"
