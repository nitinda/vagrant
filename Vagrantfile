# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 2.1.2"

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
   #config.vm.box = "nitindas/CentOS-Linux-7-x86-64"
   config.vm.box = "nitindas/centos-7.5"
   config.vm.box_version = "5.1804-1549879089"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false
   config.vm.box_check_update = true

  # config.vm.box_version = "0.0.1"
  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

   config.vm.boot_timeout = 6000

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  #config.vm.provider :virtualbox do |virtualbox, override|
  #  override.vm.box_download_checksum_type = "sha256"
  #  override.vm.box_download_checksum = "83f86355d8d1ea3001e377f67cc4a9ff15d827bea83a1878df1bcfd0a0dcab0f"
  #  override.vm.box_url = "https://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-1804_02.VirtualBox.box"
  #end

  config.vm.provider "virtualbox" do |v|
    # Customize Name of VM:
     v.name = "centos-7.5.1804-1549879089-x86-64"
    # Display the VirtualBox GUI when booting the machine
     v.gui = true
    # Customize the amount of memory on the VM:
     v.memory = "6144"
    # Customize the amount of cpu on the VM:
     v.cpus = 2
    # Customize video memory
     v.customize ["modifyvm", :id, "--vram", "128"]
    # Shared Clipboard
     v.customize ['modifyvm', :id, '--clipboard', 'bidirectional'] 
    # Enable Drag and Drop
     v.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
    # Enable Remote Display
     v.customize ["modifyvm", :id, "--vrde", "on"]
     v.customize ["modifyvm", :id, "--vrdeport", "5000,5010-5012"]
  end

  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  config.vm.provision "shell", inline: <<-SHELL
   # Enable graphical mode
  #  sudo yum -y groupinstall "GNOME Desktop"
  #  sudo systemctl set-default graphical.target
  #  sudo systemctl start graphical.target

   # Other
    sudo yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
    sudo yum -y install gcc make git python python-setuptools python-pip policycoreutils-python python-devel traceroute unzip vim wget zip unzip xorg-x11-fonts-* ncurses*
  
   # Install visual studio code
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
  #  sudo yum -y check-update
    sudo yum -y install code

   # Installing Terraform
   sudo wget https://releases.hashicorp.com/terraform/0.11.13/terraform_0.11.13_linux_amd64.zip -O /tmp/terraform_linux_amd64.zip
   sudo unzip -o /tmp/terraform_linux_amd64.zip -d /usr/local/bin/

   # Installing packer
    sudo wget https://releases.hashicorp.com/packer/1.3.3/packer_1.3.3_linux_amd64.zip -O /tmp/packer_linux_amd64.zip
    sudo unzip -o /tmp/packer_linux_amd64.zip -d /usr/local/bin/

   # Remove files
    sudo rm -f /tmp/packer_linux_amd64.zip /tmp/terraform_linux_amd64.zip

   # Install Chrome Browser
    sudo sh -c 'echo -e "[google-chrome]\nname=google-chrome\nbaseurl=http://dl.google.com/linux/chrome/rpm/stable/\\\$basearch\nenabled=1\ngpgcheck=1\ngpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub" > /etc/yum.repos.d/google-chrome.repo'
    sudo yum info google-chrome-stable
    sudo yum -y install google-chrome-stable

   # Install awscli, jinja2
    sudo pip install --upgrade awscli
    sudo pip install --upgrade jinja2
    sudo pip install --upgrade setuptools
    sudo pip install --upgrade aws-sam-cli


   # Docker
    sudo sh -c 'curl -fsSL https://get.docker.com/ | sh'
    sudo systemctl start docker
    sudo systemctl status docker
    sudo systemctl enable docker
  
   # Kubernetes
   sudo sh -c 'echo -e "[kubernetes]\nname=Kubernetes\nbaseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64\nenabled=1\ngpgcheck=1\nrepo_gpgcheck=1\ngpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg" > /etc/yum.repos.d/kubernetes.repo'
   sudo yum install -y kubectl

    # sudo usermod -aG docker $(whoami)

  SHELL

# Running Provisioners Always
# config.vm.provision "shell", run: "always" do |s|
#   s.inline = "sudo yum-complete-transaction --cleanup-only"
#  end

# Running Provisioners Always
  config.vm.provision "shell", run: "always", inline: <<-SHELL
    sudo yum update-minimal --security --bugfix
    sudo yum -y update google-chrome-stable code firefox docker-ce kubectl
    sudo chmod 666 /var/run/docker.sock
  SHELL

end