# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-SCRIPT
yum install -y bash-completion vim-enhanced
echo "Welcome to Linux System Administration I" > /etc/motd
SCRIPT

Vagrant.configure("2") do |config|

  # The guest name when using `vagrant status`
  config.vm.define "lsa-i"

  # This specifies the Vagrant box that we want to use
  config.vm.box = "centos/7"

  # Sets the hostname of the guest
  config.vm.hostname = "lsa-i"

  # Forward port 8080 on the host to port 80 on the guest while only allowing access from 127.0.0.1
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Disable folder syncing from the host to the guest
  config.vm.synced_folder '.', '/vagrant', disabled: true

  # Configuration for VirtualBox only
  config.vm.provider "virtualbox" do |vb|

    # Set the memory to 2048MB
    vb.memory = "2048"

    # Variables for additional disk filenames
    disk1 = 'disk1.vdi'
    disk2 = 'disk2.vdi'

    if (not File.exists?(disk1)) && (not File.exists?(disk2))
      # Create additional disk files
      vb.customize ['createmedium', '--filename', disk1, '--variant', 'Standard', '--size', 10240]
      vb.customize ['createmedium', '--filename', disk2, '--variant', 'Standard', '--size', 10240]

      # Adding a SATA controller that allows 2 hard drives
      vb.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 2]

      # Attaching the disks using to the SATA controller
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk1]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', disk2]
    end

  end
  
  # Provision the virtual machine
  config.vm.provision "shell", inline: $script

end
