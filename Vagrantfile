# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.ssh.insert_key = false
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

  config.vm.provision :shell, :path => ".provision/dependencies.sh", privileged: false
  config.vm.provision :shell, :path => ".provision/node.sh", privileged: false

  config.vm.network :private_network, ip: "192.168.2.2"
  config.vm.network "forwarded_port", guest: 35729, host: 35729, auto_correct: true
  config.vm.network "forwarded_port", guest: 27017, host: 37017, auto_correct: true
  for i in 8080..8100
    config.vm.network :forwarded_port, guest: i, host: i+10000, auto_correct: true
  end

  config.vm.synced_folder ".", "/vagrant", type: "virtualbox", fsnotify: true	

  config.vm.hostname = "BoK-Ionic-Box"
  config.vm.provider :virtualbox do |vb|
    vb.name = "Brandon VBox"
    vb.customize ['modifyvm', :id, '--memory', '2048']
    vb.customize ["modifyvm", :id, "--usb", "on"]
  end

end
