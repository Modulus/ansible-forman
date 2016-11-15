# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

    N = 1
    (1..N).each do |machine_id|
      config.vm.define "machine#{machine_id}" do |machine|
        machine.vm.hostname = "machine#{machine_id}"
        #machine.vm.hostname = "192.168.89.#{20+machine_id}"
        machine.vm.box = "ubuntu/trusty64"
        machine.vm.network "private_network", ip: "192.168.89.#{20+machine_id}"
        machine.vm.network "forwarded_port", guest: 9191, host: 9191, auto_correct: true
        machine.vm.network "forwarded_port", guest: 8031, host: 8031, auto_correct: true
        machine.vm.provider :virtualbox do |vb|
          vb.memory = 4096
        end
        # Only execute once the Ansible provisioner,
        # = when all the machines are up and ready.
        if machine_id == 1
          machine.vm.provision "ansible_local" do |ansible|
            # Disable default limit to connect to all the machines
            ansible.limit = "all"
            ansible.playbook = "playbook.yml"
          end
        end
      end
    end
  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
