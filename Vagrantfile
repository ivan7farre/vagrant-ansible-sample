# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

# RAM is 512 but you can tweak that here
MEMORY=512

# the instances prefix to the subnet that they use
SUBNET="192.168.10"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define :serverdev do |vmconfig|
    # Set S.O.
    vmconfig.vm.box  = "ubuntu/trusty64"
    # Custom settings db virtual machine
    vmconfig.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--cpuexecutioncap", "100"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
      vb.customize ["modifyvm", :id, "--memory", MEMORY]
      vb.name      = "serverdev"
    end
    # Set hostname & network basics.
    vmconfig.vm.hostname = "serverdev"
    vmconfig.vm.network :private_network, ip: "#{SUBNET}.10"
    vmconfig.vm.network :forwarded_port, guest: 80, host: 8080
    vmconfig.vm.network :forwarded_port, guest: 8080, host: 8081
    vmconfig.ssh.forward_agent = true
    vmconfig.ssh.insert_key    = false
    # Ansible provisioner.
    vmconfig.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.inventory_path = "provisioning/inventory"
      ansible.host_key_checking = false
      ansible.sudo = true
      ansible.verbose = "v"
    end
    # Sync deploy folder.
    vmconfig.vm.synced_folder "provisioning/", "/tmp/provisioning"
  end 
end
