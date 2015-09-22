# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.communicator = "winrm"
  config.winrm.username = 'IEUser'
  config.winrm.password = 'Passw0rd!'

  config.vm.boot_timeout = 600
  config.vm.guest = :windows

  config.vm.synced_folder "..",    "/gocd"
  config.vm.synced_folder "~/.m2", "/m2"

  config.vm.network "private_network", type: "dhcp"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = 1024*3
    vb.cpus = 4
    vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
  end

  config.vm.define 'ie9-win7' do |vm_config|
    vm_config.vm.box = "ie9-win7"
    vm_config.vm.box_url = "http://aka.ms/vagrant-win7-ie9"

    vm_config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = [
        '../infra-stuff/go-cookbooks/cookbooks',
        '../infra-stuff/go-cookbooks/shared-cookbooks/cookbooks',
        '../infra-stuff/go-cookbooks/shared-cookbooks/chef-vendor/'
      ]
      chef.roles_path     = ['../infra-stuff/go-cookbooks/roles']
      chef.add_role       'gocd_windows_vm'
    end

  end

  config.vm.define 'ie10-win7' do |vm_config|
    vm_config.vm.box = "ie10-win7"
    vm_config.vm.box_url = "http://aka.ms/vagrant-win7-ie10"

    vm_config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = [
        '../infra-stuff/go-cookbooks/cookbooks',
        '../infra-stuff/go-cookbooks/shared-cookbooks/cookbooks',
        '../infra-stuff/go-cookbooks/shared-cookbooks/chef-vendor/'
      ]
      chef.roles_path     = ['../infra-stuff/go-cookbooks/roles']
      chef.add_role       'gocd_windows_vm'
    end
  end

  config.vm.define 'ie11-win7' do |vm_config|
    vm_config.vm.box = "ie11-win7"
    vm_config.vm.box_url = "http://aka.ms/vagrant-win7-ie11"

    vm_config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = [
        '../infra-stuff/go-cookbooks/cookbooks',
        '../infra-stuff/go-cookbooks/shared-cookbooks/cookbooks',
        '../infra-stuff/go-cookbooks/shared-cookbooks/chef-vendor/'
      ]
      chef.roles_path     = ['../infra-stuff/go-cookbooks/roles']
      chef.add_role       'gocd_windows_vm'
    end
  end

  if Vagrant.has_plugin?("vagrant-omnibus")
    config.omnibus.chef_version = '12.4.2'
  end

  if Vagrant.has_plugin?('vagrant-proxyconf')
    config.proxy.http     = 'http://10.0.2.2:3128/'
    config.proxy.https    = false
    config.proxy.no_proxy = 'localhost,127.0.0.1,172.16.18.1,172.16.38.21'
  end


  if Vagrant.has_plugin?('vagrant-berkshelf')
    config.berkshelf.enabled        = false
  end

end
