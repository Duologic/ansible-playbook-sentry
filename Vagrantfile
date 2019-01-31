# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
   config.vm.provision "shell", run: "always", inline: <<-SHELL
       sudo rm /etc/localtime
       sudo ln -s /usr/share/zoneinfo/Europe/Brussels /etc/localtime
   SHELL

   ansible_groups = {
       "sentry" => ["sentry1", "sentry2"],
   }

   config.vm.define "sentry1" do |machine|
       machine.vm.box = "ubuntu/bionic64"
       machine.vm.provider "virtualbox" do |v|
           v.memory = 2048
       end
       machine.vm.hostname = "sentry1"
       machine.vm.network "forwarded_port", guest: 9000, host: 9000
       machine.vm.network "private_network", ip: "192.168.34.30"
       machine.vm.provision "shell", inline: <<-SHELL
           sudo apt-get install -y htop vim telnet curl python ntp
           #sudo ntpd -gq
       SHELL
   end

   config.vm.define "sentry2" do |machine|
       machine.vm.box = "centos/7"
       machine.vm.provider "virtualbox" do |v|
           v.memory = 2048
       end
       machine.vm.hostname = "sentry2"
       machine.vm.network "forwarded_port", guest: 9000, host: 9001
       machine.vm.network "private_network", ip: "192.168.34.31"
       machine.vm.provision "shell", inline: <<-SHELL
           sudo yum install -y epel-release
           sudo yum install -y htop vim telnet curl python ntp
           #sudo ntpd -gq
       SHELL

       machine.vm.provision :ansible do |ansible|
           ansible.groups = ansible_groups
           ansible.limit = "sentry"
           ansible.playbook = "sentry.yml"
       end
   end

end
