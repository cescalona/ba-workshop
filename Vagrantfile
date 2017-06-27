# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.define :ubuntu do |ubuntu|
    ubuntu.vm.hostname = :ubuntu
    ubuntu.vm.box = 'ubuntu/trusty64'
    ubuntu.vm.network :private_network, ip: '172.160.0.3'
    ubuntu.vm.provider :virtualbox do |vb|
      vb.gui = false
      vb.cpus = 2
      vb.memory = 1024 # works with 1024, 512 will need a swap file
    end

    # Provisioning script (install software)
    ubuntu.vm.provision :shell, inline: <<-SHELL
      DEBIAN_FRONTEND=noninteractive
      apt-get update -y
      apt-get install -y python python-dev python-pip libxml2-dev libxslt1-dev libz-dev libffi-dev libssl-dev
      pip install --upgrade pip
      python -m pip install -U setuptools
      pip install -U junos-eznc
      pip install -U distribute
      apt-get install -y software-properties-common
      apt-add-repository ppa:ansible/ansible/ansible-2.2.3
      apt-get update -y
      apt-get install -y ansible
      apt-get install -y git
    SHELL
  end

  config.vm.define :vsrx do |vsrx|
    vsrx.vm.box = "juniper/ffp-12.1X47-D15.4-packetmode"

      vsrx.vm.hostname = :vsrx
      vsrx.vm.box = 'vsrx'

      vsrx.vm.network :private_network, ip: '172.160.0.2'
      vsrx.vm.provider :virtualbox do |vb|
        vb.gui = false
        vb.cpus = 2 # needs 2 to boot?
        vb.memory = 512
      end
  end
  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
