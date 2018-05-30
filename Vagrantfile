# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/bionic64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 3000, host: 3000

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false

    # Customize the amount of memory on the VM:
    vb.memory = "4096"
  end

  config.vm.synced_folder "./", "/home/vagrant/app"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -yq curl
    sudo apt-get install -yq finger
    sudo apt-get install -yq nodejs
    sudo apt-get install -yq git
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    sudo apt-get update
    sudo apt-get install -yq nodejs
    sudo apt-get install -yq build-essential
    curl https://install.meteor.com/ | sh
    git clone https://gist.github.com/03e0dd43bcdf5623a8b1e85959c9328c.git ./app/scripts
    chmod +x ./app/scripts/download-vulcan.sh
  SHELL
end
