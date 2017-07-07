# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.define :nfsserver do |nfsserver|
    nfsserver.vm.provision :shell, inline: "echo B"
    nfsserver.vm.box = "centos/6"
    #nfsserver.vm.network "forwarded_port", guest: 8080, host: 8080
    nfsserver.vm.network "private_network", ip: "192.168.111.4"
    nfsserver.vm.synced_folder ".", "/vagrant", disabled: true
    nfsserver.vm.provider :libvirt do |libvirt|
        libvirt.memory = "512"
    end

    nfsserver.vm.provision "shell", inline: <<-SHELL
      yum -y install python2
      yum -y install libselinux-python
    SHELL

    nfsserver.vm.provision "ansible" do |ansible|
      ansible.playbook = "site.yml"
      ansible.inventory_path = "hosts"
      ansible.limit = "nfsserver"
    end
  end

  config.vm.define :nfsclient do |nfsclient|
    nfsclient.vm.provision :shell, inline: "echo B"
    nfsclient.vm.box = "centos/6"
    #nfsclient.vm.network "forwarded_port", guest: 8080, host: 8080
    nfsclient.vm.network "private_network", ip: "192.168.111.5"
    nfsclient.vm.synced_folder ".", "/vagrant", disabled: true
    nfsclient.vm.provider :libvirt do |libvirt|
        libvirt.memory = "512"
    end

    nfsclient.vm.provision "shell", inline: <<-SHELL
      yum -y install python2
      yum -y install libselinux-python
    SHELL

    nfsclient.vm.provision "ansible" do |ansible|
      ansible.playbook = "site.yml"
      ansible.inventory_path = "hosts"
      ansible.limit = "nfsclient"
    end
  end

end
