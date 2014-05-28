# vim: set ft=ruby
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure VAGRANTFILE_API_VERSION do |config|
  config.vm.box = "trusty64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  nodes = {
    apollo: "172.20.0.20",
    vulcan: "172.20.0.21",
    luna: "172.20.0.22"
  }

  config.vm.define "terminus" do |box|
    box.vm.hostname = "terminus"
    box.vm.network :private_network, ip: "172.20.0.10"

    box.vm.provision :shell, inline: "cd /vagrant && ./install-node-head"
  end

  nodes.each do |name, ip_address|
    config.vm.define name do |box|
      box.vm.hostname = name
      box.vm.network :private_network, ip: ip_address

      box.vm.provision :shell, inline: "cd /vagrant && ./install-node"
    end
  end

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end
end
