# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
    # Use Ubuntu 22.04 as the base box (you can change it to another version)
    config.vm.box = "ubuntu/jammy64"
  
    # Set the VM name and network settings
    ip_last_octet = rand(100..200)  # Random number between 100 and 200
    vm_ip = "192.168.56.#{ip_last_octet}"

    config.vm.hostname = "ubuntu-vm"
    config.vm.network "private_network", ip: vm_ip

  
    # Provisioning to set root password and allow root SSH login
    config.vm.provision "shell", inline: <<-SHELL
      echo 'root:vagrant' | sudo chpasswd
      sudo sed -i 's/.*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
      sudo sed -i 's/.*PasswordAuthentication.*/PasswordAuthentication yes/' /etc/ssh/sshd_config
      sudo systemctl restart ssh
    SHELL
  
    # Run Ansible provisioner after initial setup
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/main.yml"
      ansible.extra_vars = {
        vm_ip: vm_ip
      }
    end
  
    # Configure the VM provider (VirtualBox example)
    config.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 2
    end
  end
  