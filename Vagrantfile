# -*- mode: ruby -*-
# vi: set ft=ruby :

nodes = [
  { :hostname => 'os-gsf1',    :ip => '172.16.0.1', :box => 'ubuntu/focal64' },
  { :hostname => 'os-gsf2',    :ip => '172.16.0.2', :box => 'ubuntu/focal64' },
  { :hostname => 'os-gsf3',    :ip => '172.16.0.3', :box => 'ubuntu/focal64' },
]

Vagrant.configure("2") do |config|

  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.box = node[:box]
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]

      config.vm.provider :virtualbox do |vbox|
        vbox.memory = 513
        vbox.cpus = 1
      end

      config.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbook.yml"
        ansible.limit = "all"
        ansible.verbose = true
      end
    end
  end

end
