# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
    # Using Ubuntu server 22.04 LTS (Jammy Jellyfish) box
    config.vm.box = "generic/ubuntu2204"
  
    # Set the VM name and network settings
   # ip_last_octet = rand(100..200)  # Random number between 100 and 200
  #  vm_ip = "192.168.56.#{ip_last_octet}"
     vm_ip = "192.168.121.100"

    config.vm.hostname = "ubuntu-vm"
    config.vm.network "private_network", ip: vm_ip

  # NAT network (default)
  # Forward SSH from host 2222 -> guest 22
  config.vm.network "forwarded_port", guest: 22, host: 2222, auto_correct: true
  # Forward HTTP from host 8080 -> guest 80
  config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
  # Forward HTTPS from host 8443 -> guest 443
  config.vm.network "forwarded_port", guest: 443, host: 8443, auto_correct: true

    # Provisioning to set root password and allow root SSH login
  #  config.vm.provision "shell", inline: <<-SHELL
  #    echo 'root:vagrant' | sudo chpasswd
  #    sudo sed -i 's/.*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
  #    sudo sed -i 's/.*PasswordAuthentication.*/PasswordAuthentication yes/' /etc/ssh/sshd_config
  #    sudo systemctl restart ssh
  #  SHELL
  
    # Run Ansible provisioner after initial setup
  #  config.vm.provision "ansible" do |ansible|
  #    ansible.playbook = "playbooks/main.yml"
  #    ansible.extra_vars = {
  #      vm_ip: vm_ip
  #    }
  #  end
  
    # Configure the VM provider (Libvirt example)
    config.vm.provider :libvirt do |vb|
      vb.memory = "4096"
      vb.cpus = 4
    end
  end
  