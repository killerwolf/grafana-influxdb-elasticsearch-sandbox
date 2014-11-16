#!/usr/bin/env ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.box_check_update = true
  config.vm.network :private_network, ip: "192.168.5.111"

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--memory", "1024"]
    v.name = "influxDB"
  end
  
  config.vm.define "influxDB" do |sf2|
  end

  config.vm.hostname = "influxdb.dev"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.local.yml"
    ansible.tags = "pre-local"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.limit= "all"
    ansible.playbook = "ansible/playbook.yml"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.local.yml"
    ansible.tags = "post-local"
  end

  #config.vm.synced_folder "./", "/home/vagrant/influx", :mount_options => [ "dmode=775", "fmode=664" ], :owner => 'vagrant', :group => 'vagrant'

end

