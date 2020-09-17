# -*- mode: ruby -*-
# vi: set ft=ruby :

# Returns true if `GUI` environment variable is set to a non-empty value.
# Defaults to false
def gui_enabled?
  ENV.fetch('NOGUI', '').empty?
end

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
  config.vm.box = "ubuntu/bionic64"

  # This requires the disksize plugin.
  # Install the plugin with: vagrant plugin install vagrant-disksize
  # Set to at least 150GB for extra peace of mind (e.g plan to build an entire BSP?)
  config.disksize.size = "300GB"

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
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

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
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = gui_enabled?
    # Customize the amount of memory and CPUs on the VM:
    vb.memory = "8192"
    vb.cpus = "4"
    # Make clipboard bidirectional
    vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    apt-get update \
    && apt-get upgrade -y \
    && apt-get dist-upgrade -y \
    && apt-get autoremove -y \
    && apt-get autoclean -y
    apt-get install -y \
         build-essential \
         gcc-multilib \
         autoconf \
         autoconf-archive  \
         automake \
         autotools-dev \
         libtool \
         pkg-config \
         zsh \
         language-pack-en-base \
         gdb \
         oprofile \
         cmake \
         llvm \
         clang \
         clang-format \
         clang-tidy \
         ccache \
         bear \
         emacs \
         vim \
         vim-gtk3 \
         screen \
         byobu \
         htop \
         smem \
         mc \
         curl \
         wget \
         p7zip-full \
         gdebi \
         command-not-found \
         mercurial \
         git \
         git-extras \
         subversion \
         rabbitvcs-cli \
         rabbitvcs-gedit \
         rabbitvcs-nautilus \
         doxygen \
         meld \
         valgrind \
         ckermit \
         minicom \
         mesa-common-dev \
         libgl1-mesa-dev \
         libglu1-mesa-dev \
         libgles2-mesa-dev \
         libncurses-dev \
         libncursesw5-dev \
         libpcre3-dev \
         fonts-powerline \
         python-pip \
         virtualbox-guest-dkms \
         virtualbox-guest-utils \
         virtualbox-guest-x11 \
         default-jre
    apt-get install -y --no-install-recommends lubuntu-desktop
    snap install eclipse --classic
    snap install code --classic
    apt-get install -y qtcreator
#    rm -rf /opt/vj3rdparty
    usermod -a -G adm,dialout,cdrom,sudo,dip,plugdev vagrant
    userdel -f ubuntu
    cd /tmp && pip install --upgrade pip && pip install Jinja2 && cd -
#    rm -rf /opt/vj3rdparty
#    wget -qO- http://10.27.31.224/x-platform/downloads/vj3rdparty/amd64/vj3rdparty.tar.gz | tar xzv -C /opt
    rm -rf /home/vagrant/.oh-my-zsh && git clone https://github.com/robbyrussell/oh-my-zsh /home/vagrant/.oh-my-zsh
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git /home/vagrant/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
    git clone https://github.com/zsh-users/zsh-autosuggestions /home/vagrant/.oh-my-zsh/custom/plugins/zsh-autosuggestions
    git clone https://github.com/romkatv/powerlevel10k /home/vagrant/.oh-my-zsh/custom/themes/powerlevel10k
    wget -O /home/vagrant/.oh-my-zsh/custom/themes/bullet-train.zsh-theme http://raw.github.com/caiogondim/bullet-train-oh-my-zsh-theme/master/bullet-train.zsh-theme

    cd /tmp && wget -nv https://github.com/sharkdp/fd/releases/download/v7.4.0/fd_7.4.0_amd64.deb && gdebi -q --non-interactive fd_7.4.0_amd64.deb
    cd /tmp && wget -nv https://github.com/BurntSushi/ripgrep/releases/download/11.0.2/ripgrep_11.0.2_amd64.deb && gdebi -q --non-interactive ripgrep_11.0.2_amd64.deb
    mkdir /tmp/exa && cd /tmp/exa && wget -nv https://github.com/ogham/exa/releases/download/v0.9.0/exa-linux-x86_64-0.9.0.zip && unzip exa-linux-x86_64-0.9.0.zip && mv exa-linux-x86_64 /usr/local/bin && ln -s /usr/local/bin/exa-linux-x86_64 /usr/local/bin/exa
#    cd /tmp && wget -nv https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && gdebi -q --non-interactive google-chrome-stable_current_amd64.deb
    cd /opt && rm -rf tig && git clone https://github.com/jonas/tig && cd tig && ./autogen.sh && ./configure --prefix=/usr/local && make && make install
    wget -qO- http://10.27.31.224/x-platform/downloads/lxde/lubuntu-default-wallpaper.png > /usr/share/lubuntu/wallpapers/lubuntu-default-wallpaper.png
    wget -qO- http://10.27.31.224/x-platform/downloads/lxde/zshrc.bionic > /home/vagrant/.zshrc
    wget -qO- http://10.27.31.224/x-platform/downloads/lxde/profile > /home/vagrant/.profile
    wget -qO- http://10.27.31.224/x-platform/downloads/lxde/swap.sh | sh
    cd /opt && rm -rf fzf && git clone --depth 1 https://github.com/junegunn/fzf.git && sed -i 's|\$HOME|/home/vagrant|g' /opt/fzf/install && sed -i 's|curl\ \-|curl -s|g' /opt/fzf/install && /opt/fzf/install --xdg --completion --key-bindings --update-rc --64 --no-fish
    # NOTE: Re-downloading the .zshrc here. This is to workaround a bug in fzf's installation script
    wget -qO- http://10.27.31.224/x-platform/downloads/lxde/zshrc.bionic > /home/vagrant/.zshrc
    apt-get autoremove -y && apt-get autoclean -y
    sed -i 's/bash/zsh/g' /etc/passwd
    chown -R vagrant:vagrant /home/vagrant/
  SHELL
end
