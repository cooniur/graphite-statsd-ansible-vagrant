# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "graphite" do |graphite|
    graphite.vm.box = "chef/centos-6.6"
    graphite.vm.box_url = "https://vagrantcloud.com/chef/boxes/centos-6.6"

    graphite.vm.network :private_network, ip: "192.168.33.20"
    graphite.vm.network(:forwarded_port, {:guest=>22, :host=>2022, :id=>"ssh"})
    graphite.vm.network(:forwarded_port, {:guest=>80, :host=>18080, :id=>"grahite"})
    graphite.vm.network(:forwarded_port, {:guest=>8125, :host=>18125, :id=>"statsd"})

    graphite.vm.provision "ansible" do |ansible|
      ansible.playbook = "graphite.yml"
      ansible.sudo = true
      ansible.verbose = "vv"
    end
  end

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "1024"]
  end

end
