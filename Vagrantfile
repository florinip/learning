# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure("2") do |config|

# Defining the Puppet Master
  config.vm.define "pup" do |pup|
    pup.vm.box = "bento/centos-7.2"
    pup.vm.hostname = "puppetmaster"
    config.vm.provider "virtualbox" do |vb|
      vb.name = "pup"
      vb.memory = "2048"
      vb.cpus = 1
    end
      pup.vm.network "private_network", ip: "55.55.55.10"

      # Provisioning the Puppet Master
      pup.vm.provision "shell", inline: <<-SHELL
      sudo yum install -y lsof tree git vim ntp puppet-server httpd httpd-devel mod_ssl ruby-devel rubygems gcc gcc-c++ libcurl-devel openssl-devel
      sudo chkconfig httpd on
      sudo chkconfig ntpd on
      sudo service httpd on
      sudo service ntpd on
      sudo yum update -y
      sudo yum install kernel-devel.x86_64
      sudo /opt/VBoxGuestAdditions-5.1.10/init/vboxadd
      SHELL
  end

# Defining the Puppet Clients
  (1..3).each do |i|
    config.vm.define "test#{i}" do |test|
      test.vm.box = "bento/centos-7.2"
      test.vm.hostname = "test#{i}"
      config.vm.provider "virtualbox" do |vb|
        vb.name = "test#{i}"
        vb.memory = "1024"
        vb.cpus = 1
      end
      test.vm.network "private_network", ip: "55.55.55.1#{i}"

      # Provisioning the Puppet Clients
      test.vm.provision "shell", inline: <<-SHELL
      sudo yum install -y lsof tree git vim ntp
      sudo chkconfig ntpd on
      sudo service ntpd on
      sudo yum update -y
      sudo yum install kernel-devel.x86_64
      sudo /opt/VBoxGuestAdditions-5.1.10/init/vboxadd
      SHELL
    end
  end

end
