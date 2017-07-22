# -*- mode: ruby -*-
# vi: set ft=ruby :
$install = <<SCRIPT
# Initialize install log
rm -f /vagrant/install.log
# Configure for noninteractive mode (for dpkg)
export DEBIAN_FRONTEND=noninteractive
# Prevent accessing stdin when no terminal available in root profile
sudo sed -i 's/^mesg n/tty -s \\&\\& mesg n/g' /root/.profile
sudo ex +"%s@DPkg@//DPkg" -cwq /etc/apt/apt.conf.d/70debconf
sudo dpkg-reconfigure debconf -f noninteractive -p critical
echo "Installing Node.JS Version 6"
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - >> /vagrant/install.log
sudo apt-get install -y nodejs >> /vagrant/install.log
echo "Installing Build Essentials"
sudo apt-get install -y build-essential >> /vagrant/install.log
echo "Installing ZSH"
sudo apt-get install -y zsh >> /vagrant/install.log
echo "Installing Oh-My-Zsh"
git clone git://github.com/robbyrussell/oh-my-zsh.git /home/ubuntu/.oh-my-zsh >> /vagrant/install.log 2>&1
cp /home/ubuntu/.oh-my-zsh/templates/zshrc.zsh-template /home/ubuntu/.zshrc
# Set Theme
sed -i 's/^ZSH_THEME.*/ZSH_THEME="rkj-repos"/' /home/ubuntu/.zshrc
echo "Changing default shell to ZSH"
sudo chsh -s /usr/bin/zsh ubuntu
echo "Installing Hexo"
sudo npm install hexo-cli -g --silent >> /vagrant/install.log
if [ ! -d "/vagrant/kctechgroup.github.io" ]; then
  echo "Cloning kctechgroup.github.io"
  git clone https://github.com/kctechgroup/kctechgroup.github.io /vagrant/kctechgroup.github.io >> /vagrant/install.log 2>&1
else
  echo "Skipping clone due to preexisting folder"
fi
echo "Setting default directory"
echo "cd /vagrant/kctechgroup.github.io" >> /home/ubuntu/.zshrc
echo "Installing Hexo Dependencies"
cd /vagrant/kctechgroup.github.io
npm install --silent >> /vagrant/install.log
cd blog
npm install --silent >> /vagrant/install.log
SCRIPT

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
  config.vm.box = "ubuntu/xenial64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # BrowserSync
  config.vm.network "forwarded_port", guest: 3001, host: 3001, host_ip: "127.0.0.1"
  # Hexo Server
  config.vm.network "forwarded_port", guest: 4000, host: 4000, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

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
  config.vm.provider "virtualbox" do |vb|
    vb.linked_clone = true
    vb.memory = "1024"
  end

  # config.vm.provider "parallels" do |prl, override|
  #   override.vm.box = "parallels/ubuntu-16.04"
  #   prl.linked_clone = true
  #   prl.memory = 1024
  # end

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
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
  config.vm.provision "shell", inline: $install
end
