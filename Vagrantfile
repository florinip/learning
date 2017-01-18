# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure("2") do |config|
  #config.vm.box = "hashicorp/precise64"

  config.vm.define "pup" do |pup|
    pup.vm.box = "bento/centos-6.7"
    pup.vm.hostname = "puppetmaster"
      config.vm.provider "virtualbox" do |vb|
        vb.name = "pup"
        vb.memory = "2048"
        vb.cpus = 1 
      end
      pup.vm.network "private_network", ip: "55.55.55.10"
  end

  (1..3).each do |i|
    config.vm.define "test#{i}" do |test|
      test.vm.box = "bento/centos-6.7"
      test.vm.hostname = "test#{i}"
        config.vm.provider "virtualbox" do |vb|
          vb.name = "test#{i}"
          vb.memory = "1024"
          vb.cpus = 1
        end
      test.vm.network "private_network", ip: "55.55.55.1#{i}"
    end
  end 

end
